# UU PDP Compliance Checklist — 10 Areas

## Area 1: Data Minimisation (Pasal 16)
Only collect data that is adequate, relevant, and strictly necessary.
- Check for excessive model fields: religion, blood_type, political_leaning, ethnicity
- Check for context-aware masking of phone/NIK in non-privileged responses
- Violation: fields collected but never used in business logic
- Compliant: minimal justified fields, masking implemented

## Area 2: Explicit Consent (Pasal 20 & 21)
Processing requires explicit consent that is recorded and provable.
- Must have consent_logs table: user_id, ip_address, timestamp, policy_version, consent_given bool
- Registration must reject requests where consent_given is absent or false
- policy_version must be stored to support re-consent on policy changes
- Violation: no consent log table; user created without consent validation
- Compliant: 400/422 if no consent; consent_logs created atomically with user; IP + policy_version captured

## Area 3: Data Security & Encryption (Pasal 39)
Sensitive data (NIK, KTP, health, financial) must be encrypted at rest.
- NIK, KTP, passport, credit card fields must not be plain text in DB
- Password hashing: must be bcrypt/argon2/PBKDF2, not MD5/SHA1
- Encryption keys must come from environment variables, never hardcoded
- Violation: nik = Column(String) with no encryption; MD5 passwords
- Compliant: encrypted field type; keys from env; encrypt on write, decrypt on read

## Area 4: RBAC & Access Audit Trail (Pasal 40)
Access to personal data must be role-restricted and every access logged.
- Need role checks beyond just isAuthenticated on sensitive endpoints
- Need access_audit_logs table: who accessed whose data, when, from which IP
- Logs must be written on SUCCESSFUL access (not just failed attempts)
- Violation: sensitive endpoints only check isAuthenticated; no audit log table
- Compliant: guard/permission class checking role; audit log on each sensitive read

## Area 5: Data Portability & IDOR Protection (Pasal 7 & 13)
Users have the right to export all their data (Pasal 13). IDOR attacks violate Pasal 7.
- Must have GET /me/export or equivalent data export endpoint
- Export must verify requesting user IS the data owner (not just any authenticated user)
- Export must aggregate ALL personal data: profile, consent logs, transactions, etc.
- Violation: export uses user_id from URL without comparing to request.user.id; no export endpoint
- Compliant: 403 if requested_user_id != authenticated_user_id; structured JSON export

## Area 6: Data Breach Response (Pasal 35)
Breaches must be contained and BPPA notified within 14 calendar days.
- Need is_compromised flag or equivalent account lockout
- Compromised accounts must be blocked from sensitive endpoints (423/403)
- Need breach report generator with: incident type, affected count, data categories, discovery timestamp, containment actions
- Violation: no lockout mechanism; breach report missing required fields
- Compliant: middleware blocks is_compromised=true; report saved to DB with Pasal 35 fields

## Area 7: Data Deletion & Anonymisation (Pasal 16 & 43)
Right to erasure (Pasal 43): direct identifiers must be deleted. Transactional history may be anonymized (Pasal 16).
- Need account deletion endpoint
- Must hard-delete (not soft-delete) user personal records: User, Profile, ConsentLogs
- Financial/transaction records: anonymize (replace email with anonymous_user_XXX@deleted.invalid), do not delete
- Violation: deletion only sets is_active=false; transactions also hard-deleted; no deletion endpoint
- Compliant: hard delete PII; transactions anonymized; all in one atomic transaction

## Area 8: Consent Withdrawal (Pasal 15 & 40)
Users must be able to revoke consent (Pasal 15). Active processing must stop immediately (Pasal 40).
- Need POST /me/consent/withdraw or equivalent
- Withdrawal must create a new consent_logs entry with consent_given=false
- User account must be deactivated (is_active=false) to halt active processing
- This is DISTINCT from account deletion — historical data is retained
- Violation: no withdrawal endpoint; withdrawal updates field but no audit log; account stays active
- Compliant: new consent_logs entry with consent_given=false; is_active=false set atomically

## Area 9: Purpose Limitation (Pasal 16 & 27)
Data may only be used for purposes the user consented to (Pasal 27). Using for other purposes violates Pasal 16.
- Need marketing_consent (or equivalent) separate from registration consent
- Bulk email/newsletter must filter to marketing_consent=true only
- Dispatch endpoints must require admin/staff permission
- Violation: newsletter iterates all users regardless of marketing_consent; no opt-in field
- Compliant: filter to consented users; admin-only dispatch; marketing_consent separate from service consent

## Area 10: Data Retention Policy (Pasal 16 & 43)
Data must not be retained beyond its necessary period (Pasal 16). Must auto-purge expired records (Pasal 43).
- Need scheduled job (cron, celery beat, pg_cron) for purging old records
- Retention period must be configurable, not hardcoded
- Purge must compute cutoff as: now - retention_days
- Must log/output count of deleted records
- Violation: no purge job; retain-forever policy; purge doesn't cover all sensitive tables
- Compliant: configurable scheduled job; logs deleted count; covers audit_logs, consent_logs, session data
