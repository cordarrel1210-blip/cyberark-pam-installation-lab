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

## Lab Platform

- CyberArk PAM Self-Hosted 14.x
- VMware Workstation
- Windows Server virtual machines
- Active Directory Domain Services
- DNS and internal lab networking
- Five-VM home-lab architecture

The environment was isolated from production systems and created exclusively for training and portfolio development.

## Deployment Order

The CyberArk components were deployed in the following order:

1. Prepared the virtual infrastructure and internal network.
2. Configured the Active Directory and DNS environment.
3. Installed the CyberArk Digital Vault.
4. Installed the PrivateArk administrative client.
5. Validated the Vault through Server Central Administration.
6. Installed and connected Password Vault Web Access.
7. Ran the CPM prerequisite and pre-installation checks.
8. Installed CPM and registered it with the Vault.
9. Installed and configured the PSM component.
10. Logged into PVWA and reviewed the System Health dashboard.

Installing the Digital Vault first established the secure foundation required by the remaining CyberArk components.

## Digital Vault Installation

During the Digital Vault deployment, I:

- Prepared a dedicated Windows Server
- Used the CyberArk Vault installation media
- Supplied the required lab license file
- Configured the Vault administrator credentials
- Initialized the Vault database
- Started the Vault services
- Validated the Vault through Server Central Administration
- Connected to the environment using the PrivateArk client

Passwords, license files, recovery material, and installation media are not included in this repository.

## PVWA Installation and Configuration

During the PVWA deployment, I:

- Prepared the Windows Server and required web components
- Launched the PVWA installation wizard
- Entered the Digital Vault connection information
- Authenticated with the Vault administrative account
- Configured PVWA communication with the Vault
- Opened the Password Vault web portal
- Confirmed that PVWA appeared in System Health

## CPM Installation and Configuration

During the CPM deployment, I:

- Ran the CyberArk CPM prerequisite and pre-installation process
- Installed the Central Policy Manager
- Supplied the Vault connection information
- Registered CPM with the Digital Vault
- Started the CPM services
- Confirmed an active CPM application instance in System Health

The CPM provides password verification, change, and reconciliation capabilities for managed privileged accounts.

## PSM Installation and Configuration

During the PSM deployment, I:

- Prepared the Windows Server for privileged-session management
- Installed the PSM component
- Connected PSM to the Digital Vault
- Reviewed the purpose of PSM connection components
- Validated the component services

PSM is designed to isolate, monitor, and record privileged sessions without directly exposing managed passwords to users.

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

## Evidence Mapping

## Lab Evidence

### PVWA System Health

The System Health dashboard confirms communication with the primary Digital Vault and displays active PVWA and CPM application instances. The Vault address and URL have been redacted.

![CyberArk PVWA System Health](images/Screenshot%202026-03-30%20180436.png)

### PrivateArk Vault Connection

The PrivateArk client displays the registered Vault environment and confirms administrative connectivity.

![PrivateArk Vault connection](images/Screenshot%202026-03-30%20181022.png)

### Digital Vault Service Validation

Server Central Administration confirms successful database connectivity, Vault firewall communication, encryption configuration, and Vault service availability.

![CyberArk Vault service logs](images/Screenshot%202026-03-30%20181408.png)

| Evidence | What It Demonstrates |
|---|---|
| PVWA System Health | Primary Vault visibility and active PVWA/CPM instances |
| PrivateArk client | Successful administrative connection to the Vault |
| Server Central Administration | Vault startup, database connectivity, firewall communication, encryption configuration, and service health |

## Lessons Learned

- CyberArk components must be installed in the correct dependency order.
- DNS and network connectivity are essential for component registration.
- Each component has a distinct security responsibility.
- Service health and logs must be reviewed after installation.
- Successful portal access alone does not prove that every PAM component is healthy.
- Installation evidence must be sanitized before it is shared publicly.
- Security warnings, such as legacy certificate algorithms, should be documented and remediated rather than ignored.

## Project Scope

This project demonstrates CyberArk infrastructure deployment and component validation. Privileged-account onboarding, password rotation, Safe administration, and recorded PSM sessions will be documented as a separate advanced phase.

## Future Improvements

- Onboard a Windows privileged account
- Create and configure a Safe
- Assign Safe permissions using least privilege
- Configure a password-management platform
- Test password verification and rotation
- Launch and monitor a privileged PSM session
- Review audit and session activity
- Replace the legacy SHA-1 certificate
