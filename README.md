# 🏛️ AIT Digital Public Infrastructure Sandbox (`dpi-sandbox`)

> **Official DPI sandbox and automated deployment toolkit with identity layer, VC governance framework layer, and public web wallet.**  
> *Developed by the Asian Institute of Technology (AIT) — Supported by the Bill & Melinda Gates Foundation (Ecosystem Grant).*

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![W3C Verifiable Credentials](https://img.shields.io/badge/Standards-W3C_VC_v2.0-green.svg)](https://www.w3.org/TR/vc-data-model-2.0/)
[![OpenID OID4VCI & OID4VP](https://img.shields.io/badge/Standards-OID4VCI_%2F_OID4VP-orange.svg)](https://openid.net/)
[![Thailand ETDA & DGA](https://img.shields.io/badge/Standards-ETDA_%2F_DGA-teal.svg)](https://www.etda.or.th/)

---

## 🌐 Executive Overview

The **AIT DPI Sandbox** delivers an automated, reproducible, and disposable reference sandbox for Digital Public Infrastructure (DPI). It enables sovereign governments, universities, and ecosystem developers to evaluate and build on official **MOSIP Identity** and **Inji Verifiable Credentials (VC)** in **< 5 minutes** on a single VM at **< $30/month**.

Unlike monolithic enterprise deployments that require days of manual setup and thousands of dollars in cloud infrastructure, `dpi-sandbox` packages the complete end-to-end trust ecosystem into lightweight, standardized, and independently swappable layers strictly adhering to **100% unmodified upstream Helm charts**.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                   AIT MODULAR DIGITAL PUBLIC INFRASTRUCTURE (DPI)                      │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  📱 LAYER 4: PUBLIC GOV WALLET & APPLICATION SUITE                                     │
│  • Public Gov Wallet PWA (Zero App Store gatekeeping, WebCrypto local enclave)         │
│  • Inji Certify (Issues credentials via OID4VCI)                                       │
│  • Inji Verify (Evaluates presentation proofs via OID4VP)                              │
│                                                                                        │
│  ⚖️ LAYER 3: THAILAND TRUST FRAMEWORK & GOVERNANCE LAYER                                │
│  • In-Cluster Verifiable Data Registry (VDR) serving `did:web` and public keys         │
│  • Official Thailand ETDA & DGA JSON-LD Credential Schemas                             │
│  • VCGA Trusted Issuers Registry (TIL/TIR API) & W3C `StatusList2021` Revocation       │
│                                                                                        │
│  🪪 LAYER 2: FOUNDATIONAL IDENTITY & CITIZEN ONBOARDING                                │
│  • MOSIP Keycloak Identity & Access Management (OAuth2 / OIDC Substrate)               │
│  • MOSIP eSignet Single Sign-On Gateway (Google OAuth + Webcam Face Biometrics)        │
│  • MOSIP IDRepo & IDA (Biometric Authentication & Demographic Data Store)              │
│                                                                                        │
│  🏗️ LAYER 1: CLOUD INFRASTRUCTURE & DISPOSABLE SUBSTRATE                               │
│  • Single-Node Kubernetes Substrate (k3s / RKE2) on AWS EC2 or GCP                     │
│  • S3 Remote State Backend & DynamoDB Distributed State Locking                        │
│  • Parameter-Driven Sizing (`sizes/hackathon.tfvars`) & Automated Nightly TTL Reaper   │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🏛️ Flagship Journey: The Closed-Loop Virtual Hackathon

To ensure developer adoption and practical usability, all components integrate into a unified product lifecycle:

1. **Citizen Enrollment:** Participant authenticates via **MOSIP eSignet** (`login.id.<domain>`) using Google OAuth or in-browser Webcam Face Biometrics (ISO 30107-3 PAD liveness).
2. **Web Wallet Provisioning:** Participant receives an in-browser **Inji Web Wallet** (`wallet.egov.<domain>`) instantly—zero app store download delays or mobile device lock-in.
3. **Developer Passport VC Issuance:** **Inji Certify** issues a cryptographically signed W3C Developer Passport into their wallet containing API keys and team identity.
4. **Isolated Team Sandbox:** Cohorts build in dedicated Kubernetes namespaces partitioned with strict `NetworkPolicies`.
5. **Project Submission via Presentation Proof:** Teams submit their project to the portal by presenting their Developer Passport via **OpenID for Verifiable Presentations (OID4VP)**.
6. **Achievement Credential:** Organizers issue official tamper-evident Certificate VCs anchored in the **Trust Framework VDR**.

---

## 🚀 Quickstart & Deployment

### Prerequisites
- An AWS or GCP cloud account (or any VM with Ubuntu 22.04 LTS, 8 vCPU, 32GB RAM).
- Local tools: `terraform` (>= 1.5.0), `helm` (>= 3.12.0), `kubectl`.

### 1. Clone the Repository
```bash
git clone https://github.com/mosip-asia/dpi-sandbox.git
cd dpi-sandbox
```

### 2. Configure Your Environment
Create your configuration file from the hackathon profile:
```bash
cp sizes/hackathon.tfvars.example terraform.tfvars
```

### 3. Deploy the Sandbox
```bash
terraform init
terraform apply -var-file="sizes/hackathon.tfvars"
```

The automated provisioner executes:
* Provisions single-node CNCF `k3s` compute substrate in **< 3 minutes**.
* Pre-seeds cluster secrets and PostgreSQL schemas in **< 1 second**.
* Deploys official MOSIP Core Identity microservices (`keycloak`, `esignet`, `idrepo`, `ida`).
* Deploys Trust Framework VDR (`did:web`) and Inji credential stack via OCI Helm charts.

---

## 🌐 Multi-Agency Sovereign Domain Topology

All services are parameterized around your root domain (`${var.sandbox_domain}`) and mapped across sovereign agency boundaries:

| Agency | Subdomain | Role |
|---|---|---|
| **National Identity Authority** | `*.id.<domain>` | Citizen Onboarding (`register.id`), Keycloak (`auth.id`), eSignet SSO (`login.id`), IDA API (`ida.id`) |
| **National Trust Authority** | `*.trust.<domain>` | Schema & DID Registry (`vdr.trust`), Trusted Issuers List (`registry.trust`), Trust Console (`console.trust`) |
| **e-Government Agency** | `*.egov.<domain>` | Public Web Wallet (`wallet.egov`), Inji Certify (`issuer.egov`), Inji Verify (`verify.egov`), Hackathon Portal (`submit.egov`) |
| **Participant Teams** | `*.team-01..20.<domain>` | Wildcard ingress routing for isolated participant sandboxes |

---

## 🔒 Security & Operations

* **$0 Idle Waste (Nightly TTL Cost Reaper):** Sandboxes tag instances with expiration timestamps. An automated cron workflow discovers expired sandboxes and terminates compute instances, guaranteeing the **<$30/month** grant target.
* **Private Network Overlay (NetBird WireGuard):** Nodes optionally enroll into the center's private mesh (`100.64.0.0/16`), allowing remote cluster management and observability via central Rancher without exposing Kubernetes API ports to the public internet.

---

## 📜 Standards & Compliance

- **W3C:** [Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/), [Decentralized Identifiers (`did:web`)](https://w3c-ccg.github.io/did-method-web/)
- **OpenID Foundation:** [OpenID for Verifiable Credential Issuance (OID4VCI)](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html), [OpenID for Verifiable Presentations (OID4VP)](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
- **Thailand Standards:** Electronic Transactions Development Agency (**ETDA**) & Digital Government Development Agency (**DGA**) JSON-LD Schemas
- **Biometric & PAD Standards:** ISO/IEC 19794-5 (CBEFF demographics) and ISO/IEC 30107-3 (Presentation Attack Detection)

---

## 🗺️ Grant Milestones & 4-Month Roadmap

The project delivers **Activity 1.5** under the Gates Foundation Ecosystem Grant across 4 sequential monthly milestones:

* **Month 1 (Sep 2026) — Milestone 1.5.1: Baseline Setup:** Cloud VM substrate, centralized S3 state locking, vanilla MOSIP RDI & Inji container baseline.
* **Month 2 (Oct 2026) — Milestone 1.5.2: Lifecycle Transition & Demo:** Nightly TTL Cost Reaper, 32GB RAM tuning, Layer-1 VCGA/VDR trust, October 2026 closed-loop demo.
* **Month 3 (Dec 2026) — Milestone 1.5.3: Production Hardening & Code Freeze:** 100% Code Freeze, automated multi-tenant isolation (`team-01..20`), 3 Zero-K8s starter kits.
* **Month 4 (Jan 2027) — Milestone 1.5.4: Operational Sandbox & Gates Report:** 3-minute smoke test harness (`smoke-test.sh`), 10-team simulated dry run, Deliverable 1 Technical Report handover.

👉 **View Full WBS & Deliverable Directory:** [**`ROADMAP.md`**](ROADMAP.md)  
👉 **Interactive Sprint Board:** [**Project #14: dpi-sandbox**](https://github.com/orgs/mosip-asia/projects/14)

---

## 🤝 Contributing & Community

Contributions are welcome! Please review [`CONTRIBUTING.md`](https://github.com/mosip-asia/.github/blob/main/CONTRIBUTING.md) in the organization `.github` repository for our Definition of Done (DoD) and PR lifecycle standards.

---

## 📄 License

This project is licensed under the **Apache License 2.0** — see the [LICENSE](LICENSE) file for details.
