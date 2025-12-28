# IAM Journey: Hybrid Identity with Entra ID and SSO

## Overview
This project demonstrates the design and implementation of a **hybrid identity and access management (IAM) architecture** using on-premises Active Directory integrated with **Microsoft Entra ID**, culminating in **Single Sign-On (SSO)** for a SaaS application (Salesforce).

The lab models real-world enterprise identity practices, including directory synchronization, device registration, federated authentication, and privileged account security.

**Domain:** corp.duckdown.org (lab environment)

---

## Architecture
![Hybrid Identity Architecture](https://i.imgur.com/1pF3nGN.png)

---

## Technologies Used
- Microsoft Entra ID
- Entra Connect (Azure AD Connect)
- Windows Server 2019 (AD DS, DNS)
- Windows 11 (Hybrid Azure AD Join)
- Salesforce (SAML SSO)
- Microsoft Authenticator (MFA)

---

## On-Premises Identity Foundation
### Active Directory Deployment

- Deployed on-premises Active Directory using Windows Server 2019
- Implemented DNS and domain services to support identity authentication
- Created organizational units, users, and security groups
- Applied role-based access control via group membership

**Outcome:** Established a realistic enterprise identity foundation for hybrid integration.

<details>
<summary><strong>Implementation details</strong></summary>

- Installed AD DS and DNS using Server Manager
- Configured domain controller networking
- Joined a Windows 11 client to the domain
- Created users and assigned security groups for access control

</details>

---

## Hybrid Identity Integration
### Active Directory + Entra ID Synchronization

- Integrated on-prem AD with Microsoft Entra ID using Entra Connect
- Synchronized users and security groups to the cloud
- Enabled centralized identity management across environments
- Validated hybrid authentication from domain-joined client

**Outcome:** Unified identity lifecycle across on-premises and cloud environments.

![Hybrid Sync Architecture](https://i.imgur.com/AHfGsXu.png)

<details>
<summary><strong>Implementation details</strong></summary>

- Installed Entra Connect on the domain controller
- Connected Entra ID tenant using administrative credentials
- Configured directory synchronization scope
- Verified synchronized users and groups in Entra ID
- Enabled RDP access for domain users and validated login

</details>

---

## Seamless Single Sign-On (SSO)
### Federated Access to Salesforce

- Registered Salesforce as an Enterprise Application in Entra ID
- Configured SAML-based Single Sign-On
- Enabled federated authentication using Entra-managed identities
- Validated seamless access without re-authentication

**Outcome:** Users authenticate once via Entra ID and gain access to SaaS resources without additional login prompts.

![SSO Architecture](https://i.imgur.com/1fD8G4I.png)

<details>
<summary><strong>Implementation details</strong></summary>

- Registered hybrid-joined Windows 11 device in Entra ID
- Created Salesforce test user
- Configured SAML identifiers and reply URLs
- Downloaded SAML certificate and federation metadata from Entra ID
- Enabled SSO in Salesforce and uploaded metadata
- Validated login via incognito browser session

</details>

---

## Identity Security Hardening
### Privileged Account Protection

- Enforced Multi-Factor Authentication (MFA) on privileged Entra ID accounts
- Configured Microsoft Authenticator for admin access
- Validated MFA enforcement during Azure portal login

**Outcome:** Reduced risk associated with credential compromise and aligned with IAM security best practices.

<details>
<summary><strong>Implementation details</strong></summary>

- Enabled targeted MFA policy for global admin account
- Registered Microsoft Authenticator device
- Verified MFA challenge during privileged login

</details>

---

## What This Project Demonstrates
- Hybrid identity architecture design
- Active Directory and Entra ID integration
- SaaS federation using SAML SSO
- Privileged access security with MFA
- Enterprise IAM thinking beyond basic lab setup


