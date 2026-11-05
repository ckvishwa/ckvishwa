<div align="center">

# Vishva Teja Chikoti

### Cybersecurity &nbsp;·&nbsp; Security Engineering &nbsp;·&nbsp; QA Automation &nbsp;·&nbsp; Developer Tools

**Detection engineering, application security and test automation — each project shipped with the evidence behind its claims.**

[![Location](https://img.shields.io/badge/New_York,_NY-0F172A?style=flat-square)](#-contact)
[![MS Cybersecurity](https://img.shields.io/badge/M.S._Cybersecurity_%26_Networks-2563EB?style=flat-square)](#-education--certifications)
[![Security+](https://img.shields.io/badge/CompTIA_Security%2B-10B981?style=flat-square)](#-education--certifications)
[![Email](https://img.shields.io/badge/Email-06B6D4?style=flat-square&logo=gmail&logoColor=white)](mailto:vishvatejack@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-2563EB?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/vishvack)
[![Portfolio](https://img.shields.io/badge/Portfolio-7C3AED?style=flat-square&logo=vercel&logoColor=white)](https://system-vishva.vercel.app)

[About](#-about) &nbsp;·&nbsp; [Featured Projects](#-featured-projects) &nbsp;·&nbsp; [Security Engineering](#-security-engineering) &nbsp;·&nbsp; [QA / SDET](#-qa--sdet) &nbsp;·&nbsp; [Skills](#-technical-skills) &nbsp;·&nbsp; [Evidence](#-verified-engineering-evidence) &nbsp;·&nbsp; [Contact](#-contact)

</div>

---

## 👋 About

QA and security engineer with **18 months of enterprise QA at Cognizant Technology Solutions**
(Programmer Analyst — QA and Test Automation, Jan 2022 – Jul 2023), automating Java Selenium and
Playwright regression suites across 15+ enterprise applications, validating REST APIs with Postman
and booking data with SQL, and root-causing failures through Splunk and application logs.

Since then I completed an **M.S. in Cybersecurity & Networks** and built the six projects below to
practise the engineering side of security: writing Splunk detections against real Windows telemetry,
hardening ingestion and IAM analysis code against malformed input, and proving release gates and
inventory invariants with tests rather than with assertions in a README.

**What I care about:** fail-closed defaults, evidence you can re-run, and documentation that states
its own limits.

> Every number on this profile links to a hosted CI run, a committed detection file, or a stored
> results file. Where something is unverified, the project README says so.

---

## 🚀 Featured Projects

| Project | What it does | Core stack | Strongest verified outcome |
|---|---|---|---|
| 🛡️ **[SOC Analyst Portfolio](https://github.com/ckvishwa/soc-analyst-portfolio)** | 3-VM Active Directory detection lab: simulate from Kali, detect in Splunk, investigate as an analyst | Splunk · Sysmon · Windows Server · Kali | **8 committed SPL detections** (DET-001…008) plus 6 standalone labs and 6 investigation reports; DET-001 tuned off a forwarder false positive |
| 🧬 **[MalTrace](https://github.com/ckvishwa/Maltrace)** | Behavioral malware classifier over CAPEv2 sandbox reports, explained with SHAP and mapped to ATT&CK | Python · scikit-learn · SHAP · CAPEv2 | **Family-held-out F1 = 0.975 ± 0.008** across 37 multi-sample families, and **0 false positives on 75 benign Windows tools** |
| ⚙️ **[QualityMesh](https://github.com/ckvishwa/QualityMesh)** | Fail-closed release gate: validates CI test evidence and refuses to commit content that was never scanned | Python · pytest · Pydantic v2 · Pyright | **580 tests, 99.49% coverage** on hosted CI (3.12 + 3.14); four commit-integrity defects fixed with regression tests |
| ☁️ **[CloudShield](https://github.com/ckvishwa/Cloudshield)** | Offline GCP IAM and Kubernetes audit-log detections with repeatable rule evaluation | Python · pytest · GCP audit logs · K8s audit | **684 tests passing** on hosted CI (3.11 + 3.12); ingestion now fails closed on event-cap and deep-nesting abuse |
| 📦 **[FulfillX](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform)** | Spring Boot services for auth, products and inventory, built to test concurrency and idempotency | Java 21 · Spring Boot · PostgreSQL · Testcontainers | **61 tests** across three services on hosted CI; concurrent reservation attempts against limited stock oversell **zero** units |
| 🔐 **[Access Risk Analyzer](https://github.com/ckvishwa/access-risk-analyzer)** | Models identities and permissions as a graph and reports privilege-escalation paths to admin | Python · NetworkX · pytest | **19 tests** on hosted CI (3.10 + 3.12); dangling group/policy references and malformed effects are rejected instead of silently lowering risk |

---

## 🔒 Security Engineering

**Detection engineering.** Eight Splunk detections written against real Sysmon and Windows Security
telemetry from a 3-VM `SOCLAB.LOCAL` domain, with a dedicated Kali attacker generating genuine
cross-machine activity. Each detection has an attack-simulation document, a screenshot of it firing,
and an investigation report written from the analyst's point of view. DET-001 is the honest one: its
first version matched the Splunk Universal Forwarder's own activity, so it was baselined, narrowed,
and re-validated.

**Application security.** Across QualityMesh, CloudShield, Access Risk Analyzer and FulfillX I
audited my own code for the failure mode that matters most in security tooling — **silently
under-reporting**. Each fix is merged with a regression test that fails if the old behaviour returns:

| Repository | Weakness found | Fail-closed fix |
|---|---|---|
| [QualityMesh](https://github.com/ckvishwa/QualityMesh/pull/1) | A caller could attest a secret scan that never ran, and a staging filter could swap the scanned bytes | The orchestrator runs the scanner itself and re-verifies staged blobs before committing |
| [CloudShield](https://github.com/ckvishwa/Cloudshield/pull/1) | The event cap was applied after parsing, and deeply nested JSON raised `RecursionError` | The cap is enforced while parsing; hostile nesting becomes a handled `IngestError` |
| [Access Risk Analyzer](https://github.com/ckvishwa/access-risk-analyzer/pull/1) | A mistyped group name or an `"allow"` effect quietly dropped an admin grant | Dangling references and malformed effects raise instead of reporting lower risk |
| [FulfillX](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform/pull/3) | Any authenticated caller could release another customer's reservation | Reservation create and release are restricted to `OPERATOR`/`ADMIN`, proven by authorization tests |

**Malware analysis.** MalTrace holds out entire malware families during training rather than
splitting samples at random, because a random split measures memorisation. It reports what that test
produces, including the two samples it misses and the 27 single-sample families that cannot
demonstrate cross-sample generalisation at all.

---

## 🧪 QA / SDET

- **Enterprise regression automation** — Java Selenium and Playwright suites for airline search and
  booking workflows across 15+ applications; functional, regression, smoke and UAT cycles run through
  GitHub Actions and Jenkins.
- **API and data validation** — Python `requests` batch validation of REST APIs, Postman collections,
  SQL verification of booking data, and defect triage in Jira.
- **Concurrency and idempotency** — FulfillX proves that parallel reservation attempts against
  limited stock never oversell, and that a replayed idempotency key produces no second side effect.
- **Release assurance** — QualityMesh evaluates JUnit XML evidence before a release may proceed, and
  marks a task blocked rather than complete when its own preconditions are unmet.
- **Test-backed security fixes** — every security fix above landed with a regression test that
  reproduces the original weakness first.

---

## 🧰 Technical Skills

Each row names where the skill is demonstrated, so it can be checked.

| Area | Skills | Evidence |
|---|---|---|
| **Security Operations & Detection** | Splunk (SPL, alerts, dashboards), Sysmon, Windows Security event analysis, MITRE ATT&CK mapping, detection tuning, false-positive analysis, investigation reporting | [soc-analyst-portfolio](https://github.com/ckvishwa/soc-analyst-portfolio) |
| **Application Security** | Input-validation hardening, fail-closed design, authorization testing, JWT validation, secret-scan integrity, IDOR identification, Burp Suite, OWASP ZAP | [QualityMesh](https://github.com/ckvishwa/QualityMesh) · [CloudShield](https://github.com/ckvishwa/Cloudshield) · [FulfillX](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform) |
| **QA Automation** | pytest, JUnit 5, Testcontainers, Selenium (Java), Playwright, WebdriverIO, Postman; functional, regression, smoke, UAT and concurrency testing | [QualityMesh](https://github.com/ckvishwa/QualityMesh) · [FulfillX](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform) |
| **Backend & APIs** | Python, Java 21, Spring Boot, FastAPI, Flask, REST design, role-based access control, idempotency, PostgreSQL, SQL | [FulfillX](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform) · [MalTrace](https://github.com/ckvishwa/Maltrace) |
| **Data & Infrastructure** | GCP audit logs, Kubernetes audit logs, NetworkX graph analysis, scikit-learn, SHAP, Active Directory, BIND DNS, Kea DHCP, NFS, Linux, Windows Server | [CloudShield](https://github.com/ckvishwa/Cloudshield) · [Access Risk Analyzer](https://github.com/ckvishwa/access-risk-analyzer) · [MalTrace](https://github.com/ckvishwa/Maltrace) |
| **Developer Tooling** | GitHub Actions, Jenkins, Docker, Docker Compose, Maven, uv, Ruff, Pyright, Git, Jira, PowerShell | all repositories above |

---

## 📊 Verified Engineering Evidence

| Claim | Where it is verified |
|---|---|
| QualityMesh — 580 tests, 99.49% coverage, Python 3.12 + 3.14 | [`validate.yml` runs](https://github.com/ckvishwa/QualityMesh/actions/workflows/validate.yml) |
| CloudShield — 684 tests, Python 3.11 + 3.12 | [`ci.yml` runs](https://github.com/ckvishwa/Cloudshield/actions/workflows/ci.yml) |
| FulfillX — 61 tests across three Spring Boot services | [`pr.yml` runs](https://github.com/ckvishwa/fulfillx-enterprise-quality-platform/actions/workflows/pr.yml) |
| Access Risk Analyzer — 19 tests, Python 3.10 + 3.12 | [`ci.yml` runs](https://github.com/ckvishwa/access-risk-analyzer/actions/workflows/ci.yml) |
| MalTrace — family-held-out F1, per-fold recall and false negatives | [`family_holdout_results.json`](https://github.com/ckvishwa/Maltrace/blob/main/docs/family_holdout_results.json) · [`VALIDATION.md`](https://github.com/ckvishwa/Maltrace/blob/main/docs/VALIDATION.md) |
| MalTrace — 0 false positives across 75 benign tools | [`benign_torture_results.json`](https://github.com/ckvishwa/Maltrace/blob/main/docs/benign_torture_results.json) |
| SOC lab — 8 detections with a screenshot of each firing | [`detections/`](https://github.com/ckvishwa/soc-analyst-portfolio/tree/main/detections) · [`screenshots/`](https://github.com/ckvishwa/soc-analyst-portfolio/tree/main/screenshots) |
| Regression tests for the four security fixes above | [QualityMesh](https://github.com/ckvishwa/QualityMesh/tree/main/tests/automation) · [CloudShield](https://github.com/ckvishwa/Cloudshield/blob/main/tests/test_ingest_limits.py) · [Access Risk Analyzer](https://github.com/ckvishwa/access-risk-analyzer/blob/main/tests/test_input_integrity.py) |

All lab and sandbox work runs in isolated private environments. No project here claims production
deployment, production telemetry, or external users.

---

## 🎓 Education & Certifications

| | |
|---|---|
| **M.S. Cybersecurity & Networks** | University of New Haven, New Haven, CT — Aug 2023 – Dec 2025 |
| **B.Tech Computer Science** | Malla Reddy College of Engineering & Technology, India — Sep 2018 – May 2022 |
| **CompTIA Security+** | Oct 2026 |

---

## 📬 Contact

<div align="center">

**Open to roles in** Cybersecurity Engineering · SOC / Detection Engineering · Application Security · QA Automation / SDET · Python & Java Backend

[![Email](https://img.shields.io/badge/vishvatejack@gmail.com-06B6D4?style=for-the-badge&logo=gmail&logoColor=white)](mailto:vishvatejack@gmail.com)
[![LinkedIn](https://img.shields.io/badge/linkedin.com%2Fin%2Fvishvack-2563EB?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/vishvack)
[![Portfolio](https://img.shields.io/badge/system--vishva.vercel.app-7C3AED?style=for-the-badge&logo=vercel&logoColor=white)](https://system-vishva.vercel.app)

</div>
