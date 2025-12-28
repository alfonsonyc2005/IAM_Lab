# IAM Journey: From On-Premises to Modern Hybrid Identity with SSO
## Introduction

This portfolio documents the development of a hybrid identity and access management system for the fictional domain, corp.duckdown.org, demonstrating best practices from on-premises Active Directory setups to advanced Single Sign-On (SSO) configurations in the cloud.

What was used:
- Microsoft Entra ID
- Windows Server 2019 (DC)
- Windows 11 Client
- Organizational Units / 2 Users
- Salesforce account
- Entra Connect Sync
  
![Cloud Honeynet / SOC](https://i.imgur.com/1fD8G4I.png)


---

<br><br>



##  On-Premises Setup
### **Emulating On-Prem Active Directory Infrastructure Using Azure Services**

To replicate a realistic enterprise environment, I deployed an on-premises-style Active Directory setup in Azure using Active Directory Domain Services (AD DS).

1. **Domain Controller Configuration** - Deployed a Windows Server 2019 VM with AD DS and DNS via Server Manager.  Configured a static IP (10.0.0.4), subnet mask (255.255.255.0), and a default gateway (10.0.0.1).
2. **Client Workstation Setup** - Deployed a Windows 11 VM, joined it to the domain, and configured IP (10.0.0.5 via DHCP), subnet mask (255.255.255.0), default gateway (10.0.0.1), and DNS.
3. **Security Group Management** - Created security groups and applied role-based permissions.
4. **User Onboarding** - Added users to the domain and assigned them to appropriate security groups for access control.


![Architecture Diagram](https://i.imgur.com/1pF3nGN.png)

---


<br><br>

## Hybrid Integration
### **Setting Up Hybrid Windows Environment.**

In this setup, we configured a Windows 11 Client to join the on-premises domain, enabling centralized management and secure domain-based access. We then created Entra ID users, security groups, and assigned roles to establish cloud-based identity management. By installing and configuring Entra Connect on the domain controller, we synchronized on-premises Active Directory with Entra ID, ensuring unified identities across environments. This integration enables seamless authentication, consistent access control, and a streamlined hybrid identity infrastructure.

1. **Configured Windows 11 Client** network settings with a static DNS pointing to the domain controller and joined it to the domain.
2. **Enabled Remote Desktop Protocol (RDP) access** for domain users and verified domain login functionality.
3. **Created Entra ID users, security groups**, and assigned appropriate roles for access control.
4. **Installed Entra Connect** on the domain controller and connected it to both Entra ID and on-premises Active Directory using admin credentials.
5. **Verified successful synchronization** of on-premises users and groups into Entra ID, confirming hybrid environment integration.

![Architecture Diagram](https://i.imgur.com/AHfGsXu.png)

---

<br><br>

## Seamless Single Sign-On (SSO)
### **Setting Up a Seamless SSO in a Hybrid Windows Environment**

This project focuses on advancing the hybrid identity environment by integrating Windows 11 client into the Entra ecosystem and enabling Single Sign-On (SSO).  This strengthens the link between on-premises Active Directory and Entra ID, ensuring secure, unified access to both local and cloud resources.  By using hybrid identities, the initiative streamlines authentication, enhances security, and minimizes the need for multiple logins, creating a smoother user experience.

1. **Registering Device into Entra** - We use hybrid identity [rootadmin1@duckdown.org](mailto:rootadmin1@duckdown.org) to log into Windows 11 device, registering it within the cloud environment.  This step is crucial, as it not only brings the user identity into the hybrid fold but also extends hybrid capabilities to the device itself.
2. **Salesforce user creation** - created a user with third-party vendor, Salesforce.
3. **Entra ID SSO for Salesforce** - We start by configuring Enterprise Applications in the Entra tenant, adding Salesforce as an application SSO.
   
    - We add the Salesforce Identifier, reply URL
    - Download SAML Certificate and Federation Metadata XML
    - In Salesforce, enable SSO, upload SAML Certificate and Federation Metadata XML
    - Provision Salesforce in Microsoft Azure Enterprise Application
      
5. **Validation** - Verified by opening incognito web browser and signing into Salesforce login page with user account.  It does not ask for MFA and logs right into Salesforce.

![Architecture Diagram](https://i.imgur.com/1fD8G4I.png)

---

<br><br>


## Maintenance and Security

After setting up SSO, I went back and focused on strengthening identity security by enabling Multi-Factor Authentication (MFA) for the rootadmin1@duckdown.org account.  Previously, this highly privileged account relied only on a password for login, which posed a significant risk.  By configuring targeted MFA in Entra and setting up Microsoft Authenticator, I added an extra layer of protection to safeguard against unauthorized access.  I validated the configuration by successfully logging into the Azure Portal with MFA enforced.  This task underscores the critical role of securing privileged accounts and aligns with refining IAM practices such as enforcing password policies and ongoing access reviews.

Sensitive accounts, especially global admin roles, are prime targets for attackers.  Relying solely on password is not enough in today's threat landscape.  Regularly implementing updates, tightening security configurations like MFA, and continuously monitoring for vulnerabilities are essential to maintaining a resilient IAM system.  These proactive measures ensure that even if credentials are compromised, security controls remain in place to prevent unauthorized access, protecting both organizational data and infrastructure.

