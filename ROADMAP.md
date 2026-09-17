# 🗺️ DPI Sandbox — 4-Month Engineering Roadmap

> **Grant Activity 1.5:** Develop MOSIP and Inji VC Sandbox at AIT  
> **Sponsor:** Bill & Melinda Gates Foundation (Outcome 0)  
> **Project Board:** [**Project #14: dpi-sandbox**](https://github.com/orgs/mosip-asia/projects/14)  
> **Final Handover:** **January 30, 2027**

---

## 📊 Overview of the 4-Month Lifecycle

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│               GATES FOUNDATION GRANT ACTIVITY 1.5 WORK BREAKDOWN (WBS)                 │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  [ Month 1: 1.5.1 - Baseline Setup ] (Target: 30 Sep 2026)                             │
│  • Core Engine Baseline: Cloud VM, S3 remote state, vanilla MOSIP RDI & Inji charts.   │
│  • Target: Substrate split, central remote state locking, OCI Helm packaging.          │
│                                                                                        │
│  [ Month 2: 1.5.2 - Lifecycle Transition & Demo ] (Target: 31 Oct 2026)                │
│  • Cost Control & Trust Framework: Nightly TTL Cost Reaper, 32GB RAM tuning, VCGA TIL. │
│  • Target: October 2026 Closed-Loop Demo across citizen enrollment to VC verification. │
│                                                                                        │
│  [ Month 3: 1.5.3 - Production Hardening & Code Freeze ] (Target: 31 Dec 2026)         │
│  • Multi-Tenancy & Dev Tooling: Automated team provisioner (team-01..20), 100% freeze.│
│  • Target: 3 Zero-K8s Starter Kits, dynamic SVG credentials, ETDA compliance audit.    │
│                                                                                        │
│  [ Month 4: 1.5.4 - Operational Sandbox & Gates Report ] (Target: 30 Jan 2027)         │
│  • Production Verification & Handover: Automated 3-min smoke tests, 10-team dry run.   │
│  • Target: Submission of Deliverable 1 Technical Report to Gates Foundation.           │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📅 Milestones & Deliverables Directory

### 🟢 Month 1 — Milestone 1.5.1: Baseline Setup
**Target Date:** September 30, 2026  
**Objective:** Single-VM cloud deployment boots in < 15 minutes, S3 state is locked, and core identity/VC containers run reliably.

| Issue | Track | Title | Assignee(s) | Schedule | Status | Priority |
|:---:|:---|:---|:---|:---:|:---:|:---:|
| **[dpi-base#2](https://github.com/mosip-asia/dpi-base/issues/2)** | **Track 1 / Base Platform** | [Phase 0] GCP Organization Setup & Cloud Identity Free for `dpi.ait.ac.th` | `@akraradets` | `01 Sep – 07 Sep 2026` | `Done` | `P1 - High` |
| **[dpi-base#3](https://github.com/mosip-asia/dpi-base/issues/3)** | **Track 1 / Base Platform** | [Phase 1] Foundation Management Plane (`dpi-mgmt`) & Cloud DNS | `@akraradets` | `07 Sep – 13 Sep 2026` | `Done` | `P1 - High` |
| **[dpi-base#4](https://github.com/mosip-asia/dpi-base/issues/4)** | **Track 1 / Base Platform** | [Phase 2] Tier 1 Network Fabric (`base-vpn`) & NetBird Mesh VPN | `@akraradets` | `07 Sep – 13 Sep 2026` | `Done` | `P0 - Blocker` |
| **[dpi-base#5](https://github.com/mosip-asia/dpi-base/issues/5)** | **Track 1 / Base Platform** | [Phase 3] Tier 2 Management Plane (`base-kube-ops`) & Rancher Community | `@BossNP` | `07 Sep – 25 Sep 2026` | `In Progress` | `P1 - High` |
| **[#1](https://github.com/mosip-asia/dpi-sandbox/issues/1)** | **Track 1: Cloud Infra** | Split VM/Kube substrate from MOSIP-infra via `sizes/hackathon.tfvars` | `@parmar-m`, `@BossNP` | `15 Sep – 22 Sep 2026` | `Ready` | `P0 - Blocker` |
| **[#2](https://github.com/mosip-asia/dpi-sandbox/issues/2)** | **Track 1: Cloud Infra** | Setup centralized S3 remote state backend and DynamoDB locking in ait-mosip | `@parmar-m`, `@BossNP` | `15 Sep – 20 Sep 2026` | `Ready` | `P1 - High` |
| **[#3](https://github.com/mosip-asia/dpi-sandbox/issues/3)** | **Track 2: Foundational Identity** | Port Core MOSIP Identity & eSignet to Terraform modules (Turing approach) | `@parmar-m`, `@BossNP` | `18 Sep – 28 Sep 2026` | `Ready` | `P0 - Blocker` |
| **[dpi-nationalid#1](https://github.com/mosip-asia/dpi-nationalid/issues/1)** | **Track 2: National ID Issuer** | [DOPA] Deploy National ID Credential Issuer (Inji Certify) & Reference Verifier Example | `@thassung`, `@silanm` | `18 Sep – 28 Sep 2026` | `Ready` | `P0 - Blocker` |
| **[dpi-trust#1](https://github.com/mosip-asia/dpi-trust/issues/1)** | **Track 3: Trust Framework** | Package Thailand Trust Framework (VDR `did:web` & TIL) as OCI Helm Chart v0.1.0 | `@silanm` | `15 Sep – 25 Sep 2026` | `Ready` | `P0 - Blocker` |
| **[dpi-wallet#1](https://github.com/mosip-asia/dpi-wallet/issues/1)** | **Track 4: Public Gov Wallet** | Package Inji Stack & Web Wallet PWA as OCI Helm Chart v0.1.0 | `@thassung` | `18 Sep – 28 Sep 2026` | `Ready` | `P0 - Blocker` |
| **[dpi-base#14](https://github.com/mosip-asia/dpi-base/issues/14)** | **Track 1 / Base Platform** | Setup NetBird Mesh Enrollment Key & Rancher Cluster Import Endpoint in dpi-base | `@BossNP` | `20 Sep – 30 Sep 2026` | `Ready` | `P1 - High` |

---

### 🟡 Month 2 — Milestone 1.5.2: Lifecycle Transition & Demo
**Target Date:** October 31, 2026  
**Objective:** End-to-end issuance & OID4VP cross-verification validated against Layer-1 VCGA/VDR; Nightly Cost Reaper active ($0 waste); live demo executed.

| Issue | Track | Title | Assignee(s) | Schedule | Priority |
|:---:|:---|:---|:---|:---:|:---:|
| **[#7](https://github.com/mosip-asia/dpi-sandbox/issues/7)** | **Track 1: Cloud Infra** | Automated Nightly TTL Cost Reaper & Baked Node Image (<5m boot) | `@parmar-m`, `@BossNP` | `01 Oct – 12 Oct 2026` | `P0 - Blocker` |
| **[#8](https://github.com/mosip-asia/dpi-sandbox/issues/8)** | **Track 2: Foundational Identity** | JVM Memory Tuning (32GB RAM Target) & Dual eSignet Auth (Face PAD + Google OAuth) | `@parmar-m`, `@BossNP` | `05 Oct – 18 Oct 2026` | `P0 - Blocker` |
| **[dpi-trust#2](https://github.com/mosip-asia/dpi-trust/issues/2)** | **Track 3: Trust Framework** | VCGA Trusted Issuers List (`registry.trust`) & Trust Admin Console (`console.trust`) | `@silanm` | `05 Oct – 20 Oct 2026` | `P0 - Blocker` |
| **[#10](https://github.com/mosip-asia/dpi-sandbox/issues/10)** | **Track 4: Public Gov Wallet** | Inji Verify (`verify.egov`) & Reference University Tenant Fixtures | `@thassung`, `@silanm` | `10 Oct – 24 Oct 2026` | `P0 - Blocker` |
| **[#11](https://github.com/mosip-asia/dpi-sandbox/issues/11)** | **Track 5: Hackathon Gateway** | Citizen Registration Portal (`register.id`) & Scaffolding Virtual Hackathon Journey | `@thassung`, `@BossNP` | `12 Oct – 25 Oct 2026` | `P1 - High` |
| **[#12](https://github.com/mosip-asia/dpi-sandbox/issues/12)** | **Milestone Demo** | Confirm & Execute October 2026 Closed-Loop Demo & Interoperability Validation | `@akraradets`, `@BossNP` | `20 Oct – 31 Oct 2026` | `P0 - Blocker` |

---

### 🔵 Month 3 — Milestone 1.5.3: Production Hardening & Code Freeze
**Target Date:** December 31, 2026  
**Objective:** 100% Code Freeze; automated multi-tenant isolation (`team-01..20`), dynamic SVG templates, and ETDA/DGA standards conformance.

| Issue | Track | Title | Assignee(s) | Schedule | Priority |
|:---:|:---|:---|:---|:---:|:---:|
| **[#13](https://github.com/mosip-asia/dpi-sandbox/issues/13)** | **Track 1: Cloud Infra** | Multi-Environment CI/CD Matrix & Automated State Drift Detection | `@parmar-m`, `@BossNP` | `01 Nov – 20 Nov 2026` | `P1 - High` |
| **[#14](https://github.com/mosip-asia/dpi-sandbox/issues/14)** | **Track 2: Foundational Identity** | Stabilize `PROFILE=hackathon` & 100% Core Identity Code Freeze | `@parmar-m`, `@BossNP` | `15 Nov – 15 Dec 2026` | `P0 - Blocker` |
| **[dpi-trust#3](https://github.com/mosip-asia/dpi-trust/issues/3)** | **Track 3: Trust Framework** | ETDA & DGA Standards Alignment & Verifier Handbook Documentation | `@silanm` | `15 Nov – 10 Dec 2026` | `P0 - Blocker` |
| **[dpi-wallet#2](https://github.com/mosip-asia/dpi-wallet/issues/2)** | **Track 4: Public Gov Wallet** | Dynamic SVG Templates, Offline Credential Cache & Wallet Hardening | `@thassung` | `20 Nov – 20 Dec 2026` | `P0 - Blocker` |
| **[#17](https://github.com/mosip-asia/dpi-sandbox/issues/17)** | **Track 5: Hackathon Gateway** | Automated Team Namespace Provisioner (`team-01..20`) & Zero-K8s Starter Kits | `@BossNP`, `@thassung` | `01 Dec – 31 Dec 2026` | `P0 - Blocker` |

---

### 🟣 Month 4 — Milestone 1.5.4: Operational Sandbox Setup & Gates Report
**Target Date:** January 30, 2027  
**Objective:** Production-grade 3-min smoke tests pass 10/10; 10-team simulated dry run completed; official Deliverable 1 Technical Report submitted.

| Issue | Track | Title | Assignee(s) | Schedule | Priority |
|:---:|:---|:---|:---|:---:|:---:|
| **[#18](https://github.com/mosip-asia/dpi-sandbox/issues/18)** | **Track 1 & 2** | Automated 3-Minute Smoke Test Harness (`smoke-test.sh`) & Load Telemetry | `@parmar-m`, `@BossNP` | `01 Jan – 12 Jan 2027` | `P0 - Blocker` |
| **[#19](https://github.com/mosip-asia/dpi-sandbox/issues/19)** | **Track 3 & 4** | Cryptographic Audit Logs & End-to-End VC/VP Interoperability Verification | `@silanm`, `@thassung` | `05 Jan – 18 Jan 2027` | `P0 - Blocker` |
| **[#20](https://github.com/mosip-asia/dpi-sandbox/issues/20)** | **Track 5: Hackathon Gateway** | 10-Team Simulated Virtual Hackathon Dry Run & Teardown Verification | `@BossNP`, `@thassung` | `12 Jan – 22 Jan 2027` | `P0 - Blocker` |
| **[#21](https://github.com/mosip-asia/dpi-sandbox/issues/21)** | **Grant Governance** | Finalize & Submit Deliverable 1 Technical Report to Gates Foundation | `@akraradets` | `15 Jan – 30 Jan 2027` | `P0 - Blocker` |

---

## 🎯 Track Ownership Directory

| Track | Name | Lead(s) | Focus Area |
|---|---|---|---|
| **Track 1** | **Cloud Infra & GitOps Automation** | Mehul & K. Boss | Terraform modules, S3 remote state, DynamoDB locking, Nightly TTL Cost Reaper (<$30/mo), CI/CD runners. |
| **Track 2** | **Foundational Identity & National ID Issuer** | Mehul & K. Boss | `sizes/hackathon.tfvars`, Keycloak, IDRepo, IDA, BioSDK, eSignet (Webcam Face PAD), Inji Certify DOPA issuer (`dpi-nationalid`). |
| **Track 3** | **Thailand Trust Framework (VCGA & VDR)** | Sila | In-cluster VDR (`did:web`), VCGA Trusted Issuers List (TIL), W3C `StatusList2021` revocation, ETDA/DGA JSON-LD schemas (`dpi-trust`). |
| **Track 4** | **Public Gov Wallet & Credentials** | Nathas & Sila | Citizen Inji Web Wallet PWA (`dpi-wallet` at `wallet.egov`), dynamic SVG cards, Inji Verify (`verify.egov`), zero-phone-home verification. |
| **Track 5** | **Hackathon Gateway & Dev Toolkit** | Integration Track | Campaign Landing Page (`www.egov`), Citizen Registration (`register.id`), multi-tenant namespaces (`team-01..20`), Zero-K8s Starter Kits. |
