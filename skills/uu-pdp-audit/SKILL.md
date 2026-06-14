---
name: uu-pdp-audit
description: >
  Conducts a full UU PDP (Indonesian Personal Data Protection Law) compliance audit on a codebase and generates a prioritized Markdown report with findings and fix suggestions. Use this skill whenever a user wants to: audit their app for UU PDP compliance, check if their system follows Indonesian data protection law, do a self-assessment for PDP, find out which parts of their code violate UU PDP, or get a privacy/data protection compliance report. Triggers on any mention of UU PDP, PDP compliance, data protection audit, Indonesia privacy law, or similar.
---

# UU PDP Compliance Audit Skill

You are an expert in Indonesian data protection law (UU PDP No. 27 Tahun 2022) and software security. Your task is to audit a codebase for UU PDP compliance and automatically produce a saved Markdown report.

## UU PDP Pasal Reference — Use This Exactly

Always cite these specific pasal numbers. Never cite Pasal 57-72 (those are criminal sanction articles, not rights or obligation articles).

| Area | Correct Pasal to Cite |
|------|-----------------------|
| Data Minimisation | Pasal 16 |
| Explicit Consent (lawful basis) | Pasal 20 |
| Consent must be recorded | Pasal 21 |
| Data subject right to access & portability | Pasal 7 & Pasal 13 |
| Data Security / Encryption obligation | Pasal 39 |
| Controller access control obligation | Pasal 40 |
| Data Breach notification (14 days to BPPA) | Pasal 35 |
| Right to Erasure / Deletion | Pasal 16 & Pasal 43 |
| Consent Withdrawal | Pasal 15 & Pasal 40 |
| Purpose Limitation | Pasal 16 & Pasal 27 |
| Data Retention / Purge obligation | Pasal 16 & Pasal 43 |

## The 10 Compliance Areas

Read `references/uu-pdp-reference.md` for the full checklist per area before starting.

1. **Data Minimisation** (Pasal 16)
2. **Explicit Consent** (Pasal 20 & 21)
3. **Data Security & Encryption** (Pasal 39)
4. **RBAC & Access Audit Trail** (Pasal 40)
5. **Data Portability & IDOR Protection** (Pasal 7 & 13)
6. **Data Breach Response** (Pasal 35)
7. **Data Deletion & Anonymisation** (Pasal 16 & 43)
8. **Consent Withdrawal** (Pasal 15 & 40)
9. **Purpose Limitation** (Pasal 16 & 27)
10. **Data Retention Policy** (Pasal 16 & 43)

## Audit Process

### Step 1: Understand the Codebase

Build a map of the application before checking anything:
- What kind of app? (web API, monolith, microservices, mobile backend, government system, etc.)
- Tech stack? (language, framework, ORM, database)
- What personal data does it handle? Look for: user models, profile fields, NIK/KTP, phone, email, address, health/financial records
- Find: models/entities, API endpoints, auth/authorization code, background jobs, data export flows, logging config

Use `find`, `grep`, and file reads to explore. Start broad (file tree, key model files) then zoom in.

**When no codebase is provided:** treat the user's description as the complete picture. Reason about what a typical app of that stack looks like. Flag anything not mentioned as "Unknown / likely missing — verify and implement if absent."

### Step 2: General Security Assessment

Baseline security check independent of UU PDP:
- Password hashing algorithm (must be bcrypt/argon2/PBKDF2, not MD5/SHA1)
- Session/token management and expiry
- Are sensitive endpoints protected? Any publicly accessible sensitive routes?
- Hardcoded secrets or API keys in source code — if found, report ONLY the file path and line number, never reproduce the actual secret value (write `[REDACTED]` in place of the value)
- Error responses leaking stack traces
- Sensitive fields (passwords, NIK, tokens) appearing in logs

### Step 3: UU PDP Assessment

For each of the 10 areas, find evidence of compliance or violation. Cite file paths and line numbers. Determine:
- Compliant — implemented correctly
- Partial — some implementation but incomplete or with gaps
- Non-compliant — missing or clearly wrong
- Unknown — not mentioned/found; flag for manual verification

**Priority assignment:**
- HIGH: Missing consent, unencrypted NIK/KTP, no access control on sensitive data, no breach response — direct legal liability
- MEDIUM: Incomplete audit trails, missing portability endpoint, incomplete anonymisation, no retention policy
- LOW: Partial implementations that could be stronger, documentation gaps

### Step 4: Save the Report Automatically

**Do not wait for the user to ask — always save the report immediately after completing the audit.**

Determine the save location in this order:
1. If a real codebase was inspected: save as `pdp_audit_report.md` in the project root
2. If no codebase path was given: save as `pdp_audit_report.md` in the current working directory
3. If neither is clear: save to `~/pdp_audit_report.md`

After saving, tell the user the exact file path where the report was saved.

Use the structure in `references/report_template.md`. The template includes a "Panduan Membaca" (reading guide) at the top that explains all status symbols and priority levels — always include this section so any reader can understand the report without prior context.

## Writing the Report

**Cite the correct Pasal.** Use the table at the top of this skill. Never cite Pasal 57-72 to describe obligations or rights — cite those only when explaining potential penalties.

**Be concrete, not generic.** Every finding must reference actual code (file:line) or — when no code is available — show a specific code example in the user's stack demonstrating what to implement. **Exception: never reproduce actual secret values, tokens, passwords, or credentials found in code — always replace them with `[REDACTED]` in any code snippet or citation.**

**Speak to founders, not lawyers.** Explain why each item matters in plain language.

**Cover all 10 areas every time.** If something is not mentioned by the user, mark it Unknown and explain what to check — do not skip it.
