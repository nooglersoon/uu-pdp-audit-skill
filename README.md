# UU PDP Audit Skill 🛡️

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![UU PDP](https://img.shields.io/badge/UU%20PDP-No.%2027%2F2022-blue)](https://peraturan.bpk.go.id/Details/229798/uu-no-27-tahun-2022)
[![ISO 27001](https://img.shields.io/badge/ISO-27001-blue)](https://www.iso.org/isoiec-27001-information-security.html)

Claude skill that audits your codebase for compliance with **UU PDP (Undang-Undang Pelindungan Data Pribadi No. 27 Tahun 2022)** — Indonesia's comprehensive personal data protection law, similar to GDPR.

Point Claude at your codebase (or just describe your stack), and it will produce a complete, prioritized Markdown audit report covering all 10 compliance areas — automatically saved to your project.

Credits to https://github.com/kertijayancom/pdp-koans-django for the UU PDP Summary as the reference.

---

## Quick Start

```bash
npx skills add nooglersoon/uu-pdp-audit
```

Then in Claude Code, describe your app:

> Audit aplikasi saya untuk compliance UU PDP. Tech stack: NestJS + PostgreSQL. Kami punya user registration, tapi belum ada consent logging dan belum ada endpoint untuk user hapus datanya.

Or point it at a real codebase:

> Please do a full UU PDP compliance audit on this repository.

Claude will read through your code, check all 10 compliance areas, and **automatically save** `pdp_audit_report.md` to your project root.

---

## What Gets Audited

The skill checks all 10 areas mandated by UU PDP, each mapped to the correct legal article:

| # | Area | Pasal UU PDP |
|---|------|--------------|
| 1 | **Data Minimisation** — Are you collecting only what you need? | Pasal 16 |
| 2 | **Explicit Consent** — Is consent recorded with timestamp, IP, and policy version? | Pasal 20 & 21 |
| 3 | **Data Security & Encryption** — Is NIK/KTP/sensitive data encrypted at rest? | Pasal 39 |
| 4 | **RBAC & Access Audit Trail** — Who can access sensitive data, and is it logged? | Pasal 40 |
| 5 | **Data Portability & IDOR Protection** — Can users export their own data safely? | Pasal 7 & 13 |
| 6 | **Data Breach Response** — Do you have a 14-day BPPA notification plan? | Pasal 35 |
| 7 | **Data Deletion & Anonymisation** — Can users request account deletion? | Pasal 16 & 43 |
| 8 | **Consent Withdrawal** — Can users revoke consent and stop data processing? | Pasal 15 & 40 |
| 9 | **Purpose Limitation** — Is data used only for its stated purpose? | Pasal 16 & 27 |
| 10 | **Data Retention Policy** — Do you auto-purge data past its retention period? | Pasal 16 & 43 |

---

## Sample Report Output

The skill generates a structured Markdown report saved automatically to your project:

```
pdp_audit_report.md
```

<img width="782" height="738" alt="Screenshot 2026-06-14 at 08 25 55" src="https://github.com/user-attachments/assets/2cd4e6c4-9d62-42b7-a4b3-5a15437bdb08" />


The report includes:

- **📖 Reading Guide** — explains status symbols (✅ ⚠️ ❌ ❓) and priority levels (🔴 HIGH / 🟡 MEDIUM / 🟢 LOW) so any team member can understand it
- **Executive Summary** — overall compliance posture at a glance
- **General Security Assessment** — password hashing, secrets management, endpoint exposure
- **10-area UU PDP deep-dive** — findings with code evidence, correct Pasal citations, and stack-specific fix recommendations
- **Prioritized Action Plan** — ordered by legal urgency with estimated effort

---

## Supported Tech Stacks

Works with any stack. Provides stack-specific code examples for:

- **Node.js / Express / NestJS** — middleware patterns, TypeORM, Sequelize, Knex
- **Next.js** — API Routes, Server Actions, Supabase RLS
- **Golang** — Gin, Echo, Fiber, GORM hooks
- **Django / Laravel / Rails** — ORM-level encryption, management commands
- And any other backend — falls back to framework-agnostic patterns

---

## Who Is This For?

- **Startup founders** who need to self-assess before launching in Indonesia
- **CTOs** preparing for a compliance audit or investor due diligence
- **Dev teams** building HRIS, school management systems, or government apps — the highest-risk app categories under UU PDP
- **Agencies** building SaaS products for Indonesian clients

---

## Legal Disclaimer

This tool performs automated code analysis to help identify potential compliance gaps. It is **not a substitute for legal advice**. Findings marked ❓ require manual verification. Consult a qualified data protection lawyer for formal compliance certification.

UU PDP enforcement is handled by **BPPA (Badan Pelindungan Data Pribadi)**. Non-compliance can result in:
- Administrative fines up to **2% of annual global revenue**
- Criminal penalties for severe violations

---

## Contributing

Contributions are welcome! The skill covers 10 areas today. If you spot a missing check, incorrect Pasal citation, or want to add framework-specific guidance:

1. Fork this repo
2. Edit `skills/uu-pdp-audit/SKILL.md` or the reference files under `skills/uu-pdp-audit/references/`
3. Open a pull request with a description of what you changed and why

Please keep Pasal citations accurate — incorrect legal references are the most harmful type of error in this tool.

---

## Repository Structure

```
uu-pdp-audit/
├── skills/
│   └── uu-pdp-audit/
│       ├── SKILL.md                  # Main skill instructions for Claude
│       └── references/
│           ├── uu-pdp-reference.md   # Detailed checklist for all 10 UU PDP areas
│           └── report_template.md    # Markdown report template with legend
├── LICENSE
└── README.md
```

---

## References

- [UU No. 27 Tahun 2022 tentang Pelindungan Data Pribadi](https://peraturan.bpk.go.id/Details/229798/uu-no-27-tahun-2022)
- [BPPA — Badan Pelindungan Data Pribadi](https://bppa.go.id)
- [PDP Koans (Django Edition)](https://github.com/kertijayancom/pdp-koans-django) — the TDD learning platform that inspired this skill's 10-area framework
