# cyberark-pam-installation-lab
Self-hosted CyberArk PAM lab documenting Vault, PVWA, CPM, and PSM installation, component connectivity, and security validation.
# CyberArk PAM Installation Lab

## Overview

This project documents the deployment and validation of a self-hosted CyberArk Privileged Access Management (PAM) environment.

The lab was designed to develop hands-on experience with CyberArk architecture, component installation, Vault connectivity, privileged-access infrastructure, and security validation.

> This repository contains sanitized lab documentation only. CyberArk software, license files, passwords, configuration backups, and proprietary installation materials are not included.

## Lab Objectives

- Deploy the core CyberArk PAM components
- Configure communication between the CyberArk components
- Validate access to the Password Vault Web Access portal
- Confirm Vault and CPM service connectivity
- Review Vault startup and security logs
- Understand the responsibilities of each PAM component
- Document security risks and recommended remediation

## Environment Architecture

| System | Purpose |
|---|---|
| Domain Controller | Provides Active Directory and DNS services |
| Digital Vault | Securely stores privileged credentials and audit data |
| PVWA | Provides the web interface for CyberArk users and administrators |
| CPM | Manages and rotates privileged-account passwords |
| PSM | Monitors and records privileged sessions |
| Router | Provides network connectivity between lab systems |

## CyberArk Components

### Digital Vault

The Digital Vault acts as the protected storage location for privileged credentials, platform data, policies, and audit records.

During validation, the Vault successfully:

- Connected to its database
- Loaded its object cache
- Opened communication through the Vault firewall
- Started its primary services
- Used AES-256 and RSA-2048 encryption

### Password Vault Web Access

PVWA provides the browser-based interface used to manage privileged accounts, Safes, platforms, policies, and administrative settings.

I successfully accessed the PVWA portal and verified that it could communicate with the primary Vault and CPM environment.

### Central Policy Manager

The CPM manages privileged-account passwords according to the assigned platform policy. Its responsibilities include:

- Password verification
- Automated password changes
- Credential reconciliation
- Password-policy enforcement

The lab’s System Health dashboard confirmed an active CPM application instance.

### Privileged Session Manager

PSM provides isolated access to privileged systems while supporting session monitoring and recording. In an enterprise environment, PSM reduces the need to expose privileged credentials directly to end users.

## Installation Summary

1. Prepared the Windows Server virtual machines and network connectivity.
2. Installed and configured the CyberArk Digital Vault.
3. Connected to the Vault using the PrivateArk client.
4. Installed and configured PVWA.
5. Installed CPM and connected it to the Vault.
6. Prepared the PSM server for privileged-session management.
7. Accessed the PVWA portal.
8. Reviewed the System Health dashboard and Vault server logs.
9. Verified component communication and service availability.

## Validation Results

The following results confirmed that the environment was operational:

- PrivateArk displayed the registered Vault environment
- PVWA successfully loaded in the browser
- The System Health page detected the primary Vault
- PVWA showed an active web application instance
- CPM showed an active application instance
- Vault logs confirmed successful database connectivity
- Vault firewall communication was enabled
- Core Vault services reported as running

## Security Finding

During log review, the Vault reported that its certificate used the legacy SHA-1 signature algorithm.

SHA-1 is no longer recommended because of known collision weaknesses. In a production environment, I would replace the certificate with one using SHA-256 or stronger, validate the certificate chain, and confirm that every CyberArk component trusted the replacement certificate.

## Security Practices

- Sensitive hostnames and IP addresses were removed from screenshots
- Passwords and privileged credentials were not recorded
- CyberArk license files and installation packages were not published
- Configuration backups and recovery material were excluded
- Screenshots were reviewed before publication
- The environment was isolated for lab use

## Skills Demonstrated

- CyberArk PAM architecture
- Digital Vault installation and validation
- PVWA configuration
- CPM connectivity and password-management concepts
- PSM architecture and session-management concepts
- Windows Server administration
- Virtual-machine networking
- Service and log validation
- Security finding analysis
- Technical documentation

## Lab Evidence

Sanitized screenshots demonstrating the completed environment are included in the `images` directory.

## Future Improvements

- Onboard a Windows privileged account
- Create and configure a Safe
- Assign Safe permissions using least privilege
- Configure a password-management platform
- Test password verification and rotation
- Launch and monitor a privileged PSM session
- Review audit and session activity
- Replace the legacy SHA-1 certificate
