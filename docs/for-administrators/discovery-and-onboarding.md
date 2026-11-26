# PAM 2.0 Windows Device Onboarding Through Discovery

## Purpose

This document describes the configuration and process used to automatically onboard Windows servers into Delinea Secret Server through Discovery.

The onboarding process identifies eligible Windows servers from Active Directory, performs discovery using the approved scanning identity, and automatically creates managed assets within Delinea Secret Server.

---

## Discovery Scope

| Item | Value |
|--------|--------|
| Active Directory Domain | `vccnet.volvocars.net` |
| Discovery Scope | `vccnet.volvocars.net/CS/Servers/` |
| Discovery Method | Active Directory Discovery |
| Scanning Service Identity | `BPPPAMWD` |
| Target Platform | Windows Servers |
| PAM Solution | Delinea Secret Server |

### Discovery Scope Definition

The Discovery Engine is configured to scan Windows computer objects located under the following Active Directory Organizational Unit (OU):

```text
vccnet.volvocars.net/CS/Servers/
```

Only servers within this scope are evaluated for onboarding into Delinea Secret Server.

---

## Discovery Account

The Discovery Engine uses the following service identity to perform host discovery and account validation:

| Setting | Value |
|----------|---------|
| Service Account | `BPPPAMWD` |
| Purpose | Discovery and account validation |
| Required Access | Local Administrator on target servers |
| Authentication | Active Directory |

The required permissions for this account are provisioned through the GPOs defined in this document.

---

## Automated Onboarding Rule

### Onboarding Logic

A Delinea Discovery Rule is configured to automatically onboard discovered Windows hosts when a designated local administrative account is detected.

| Condition | Action |
|------------|------------|
| Host platform detected as Windows | Continue evaluation |
| Local account contains `vorlvop27` | Eligible for onboarding |
| Discovery succeeds | Create managed asset |
| Asset created | Place in Windows Folder |
| Access assignment | Grant Infra Team administrative permissions |

### Rule Definition

```text
IF:
  Host Type = Windows
  AND
  Account Name contains "vorlvop27"

THEN:
  Onboard Host
  Place Asset in Windows Folder
  Grant Infra Team Administrative Access
```

### Result

When Discovery identifies a Windows server within the configured Active Directory scope and detects the `vorlvop27` account:

1. The host is automatically onboarded into Delinea Secret Server.
2. A managed asset is created in the designated Windows folder.
3. Infra Team administrative permissions are assigned.
4. The host becomes available for PAM lifecycle operations, including:
   - Password rotation
   - Credential management
   - Access governance
   - Session management (where applicable)

---

## Confirmed PAM Discovery Design

| Item | Confirmed Value |
|--------|--------|
| Discovery Scope | `vccnet.volvocars.net/CS/Servers/` |
| Scanning Service Identity | `BPPPAMWD` |
| Discovery Account Access | Local Administrator |
| Discovery Engine Connectivity | Approved Discovery Engine source IPs |
| Onboarding Trigger Account | `vorlvop27` |
| Target Folder | Windows Folder |
| Access Model | Infra Team Administrator Access |
| Discovery Platform | Delinea Secret Server Discovery |

---

## Discovery Validation

Validate the following after configuration and deployment.

### Active Directory Discovery

- Confirm the Discovery Engine can enumerate computer objects within:

```text
vccnet.volvocars.net/CS/Servers/
```

- Confirm target servers are returned in discovery results.

### Host Discovery

Verify that the `BPPPAMWD` account can:

- Authenticate to the server.
- Enumerate local accounts.
- Query local administrative groups.
- Validate Windows platform information.

### Automated Onboarding Rule

- Confirm a test server containing the `vorlvop27` account is discovered.
- Confirm the server is automatically onboarded.
- Confirm the asset is created in the Windows Folder.
- Confirm Infra Team permissions are assigned correctly.
- Confirm the asset is ready for password management and governance activities.

---

## Prerequisites

The following GPOs must be implemented and validated before onboarding can succeed:

1. `GPO-Servers-PAM-ScannerAccess`
2. `GPO-Servers-PAM-RemoteSAM`
3. `GPO-Servers-PAM-RPCFirewall`

These GPOs ensure that:

- The Discovery account (`BPPPAMWD`) can access managed servers.
- Remote SAM queries required for account discovery are permitted.
- Firewall rules allow communication from approved Discovery Engine source IPs.
- Discovery and onboarding activities operate within Volvo Cars security requirements.
