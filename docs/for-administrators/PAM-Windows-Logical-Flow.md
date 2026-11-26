# PAM 2.0 Windows Privileged Access Logical Architecture

## Purpose

This document describes how privileged access to Windows systems is governed through Delinea Secret Server, Microsoft Entra ID, Active Directory, Cyolo Session Manager, and Distributed Engines.

## Logical Overview

```mermaid
flowchart LR
    User[Authorized User]
    Entra[Microsoft Entra ID
SSO + MFA]
    Delinea[Delinea Secret Server]
    Cyolo[Cyolo Session Manager]
    AD[Active Directory]
    DE[Delinea Discovery Engines]
    Windows[Managed Windows Servers]

    User --> Entra
    Entra --> Delinea
    Delinea --> Cyolo
    Cyolo --> Windows
    AD --> Windows
    DE --> Windows
    DE --> Delinea
```
## Logical flows

### Discovery

Delinea Discovery Engines scan approved Windows servers using the permitted network path and approved scanning identity. Discovered Windows servers and accounts are reviewed before onboarding.

### Credential management

Delinea stores and governs the credential for `volvop27`. Only Delinea generates, rotates, verifies, and retains password history for the account.

### User access

An authorized user authenticates through Entra ID SSO and MFA, supplies the required justification and ticket reference, obtains access under the applicable approval model, and launches a controlled Cyolo session to an authorized target.

## Component Responsibilities

| Component | Responsibility |
|------------|------------|
| Delinea Secret Server | Credential storage, retrieval, rotation, audit |
| Discovery Engines | Windows discovery and management |
| Microsoft Entra ID | Authentication and MFA |
| Active Directory | Authorization and policy |
| Cyolo Session Manager | Session brokering |
| Windows Servers | Managed endpoints |

## Discovery Flow

```mermaid
flowchart LR
    DE[Distributed Engine] --> WIN[Windows Servers]
    DE --> SS[Delinea Secret Server]
```

## Credential Management Flow

```mermaid
sequenceDiagram
    participant Delinea
    participant Windows
    Delinea->>Windows: Verify Credential
    Delinea->>Windows: Rotate Password
    Windows-->>Delinea: Success Status
```

## User Access Flow

```mermaid
sequenceDiagram
    participant User
    participant Entra
    participant Delinea
    participant Cyolo
    participant Server
    User->>Entra: SSO + MFA
    User->>Delinea: Request Access
    Delinea->>Cyolo: Authorize Session
    Cyolo->>Server: Launch Session
```

## Responsibility Boundary

| Function | Owner |
|------------|------------|
| Password Generation | Delinea |
| Password Rotation | Delinea |
| Credential Storage | Delinea |
| User Authentication | Entra ID |
| Authorization | Delinea + AD |
| Session Connectivity | Cyolo |
| Discovery | Distributed Engines |

## Security Constraints

- Delinea and Microsoft LAPS must not manage the same account simultaneously.
- Password rotation must only be enabled after LAPS ownership has been removed.
- Historical password access must be audited.
- Credentials must never be stored in emails, tickets, chats, or documentation.
