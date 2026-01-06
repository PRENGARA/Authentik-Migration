# Lessons Learned: Migrating from Keycloak to Authentik with SAML

## Introduction
Migrating identity providers is a critical task in enterprise environments. This lab focused on replacing Keycloak with Authentik and integrating services like GlobalProtect and Snipe-IT using SAML authentication.

## Key Learnings
### 1. TLS and PKI
- Secure communication starts with proper TLS configuration.
- Using a trusted Root CA and applying certificates under Authentik's *System → Certificates* ensures browser trust and prevents MITM attacks.

### 2. LDAPS Sync with Active Directory
- LDAPS requires importing the CA certificate and disabling StartTLS.
- Service accounts and correct Base DN settings are essential for syncing users and groups.

### 3. SAML Integration for GlobalProtect and Snipe-IT
- GlobalProtect IdP profile must include Authentik's SSO and SLO URLs.
- Snipe-IT requires accurate ACS URL and Entity ID mapping.
- Common pitfalls: clock skew, incorrect metadata, and certificate mismatches.

### 4. NAT and Security Policies
- External access to Authentik demands proper NAT and firewall rules.
- Policies must allow traffic from the untrust zone to the Authentik host.

## Troubleshooting Tips
- **Certificate Chain Issues:** Verify intermediate and root CA installation.
- **LDAP Connectivity:** Test LDAPS with `openssl s_client` before configuring Authentik.
- **SAML Errors:** Check logs for ACS URL mismatches and validate metadata XML.

## Best Practices
- Use implicit consent flows for SAML apps.
- Regularly monitor authentication logs for anomalies.
- Document all configuration steps for reproducibility.

## Conclusion
This lab reinforced the importance of secure identity management and highlighted practical challenges in integrating multiple services with a new IdP. Mastering these steps prepares you for real-world IAM migrations.
