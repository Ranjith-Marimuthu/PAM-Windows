# Active Directory and GPO Configuration

**Purpose:** Define the AD structure and three PAM GPO requirements for Windows breakglass management.  
**Audience:** Active Directory administrators, Group Policy administrators, Windows engineers, and PAM administrators.

## Confirmed AD design

| Item | Confirmed value |
|---|---|
| Target OU | `vccnet.volvocars.net/CS/Servers/PROD` |
| Scanning group | `Server-PAM-ScanningAccount` |
| Scanning service identity | `BPPPAMWD` |
| Production target group | `Server-PAM-Prod` |
| Security filtering | `Server-PAM-Prod` contains approved production server computer objects |

`Server-PAM-Prod` provides GPO security filtering for approved production target servers.

## Required GPOs

| GPO | Purpose |
|---|---|
| GPO-Servers-PAM-ScannerAccess | Permit the approved scanning identity to access target servers and become an effective Administrators member |
| GPO-Servers-PAM-RemoteSAM | Permit approved remote SAM calls from the scanning identity |
| GPO-Servers-PAM-RPCFirewall | Permit required PAM traffic only from approved Discovery Engine source addresses |

## GPO-Servers-PAM-ScannerAccess

### Required configuration

| Setting | Required value |
|---|---|
| Policy area | Access this computer from the network |
| Principal | `Server-PAM-ScanningAccount` |
| Local group | Administrators (built-in) |
| Member action | Update |
| Member | `Server-PAM-ScanningAccount` |

### Scope and filtering

1. Link the GPO only to the approved target OU or a more specific approved child OU.
2. Use `Server-PAM-Prod` for computer-object security filtering.
3. Exclude or block inheritance for unapproved systems where organizational OU policy permits it.
4. Confirm that Enforced, Block Inheritance, and WMI filters do not cause unintended policy application.

### Policy conflicts

Before deployment:

1. Export or document the current effective settings.
2. Search for competing User Rights Assignment policies and Restricted Groups policies.
3. Identify GPO precedence and cross-OU inheritance.
4. Determine whether another policy replaces the Administrators membership.

### Validation

1. Run `gpupdate /force` on an approved test server.
2. Run `gpresult /h` and review the generated HTML report.
3. Run `whoami /groups` or the equivalent effective-group validation as an approved method.
4. Confirm `Server-PAM-ScanningAccount` is represented in the network logon right.
5. Confirm it is present in the local Administrators built-in group.
6. Re-run validation from the assigned Discovery Engine.

### Rollback

1. Remove or restore the GPO link only after change approval.
2. Restore the previous Administrators and User Rights Assignment configuration.
3. Run Group Policy update on affected targets.
4. Revalidate effective policy and discovery connectivity.

### Evidence

- GPO settings export.
- Security filtering and link scope screenshot or export.
- `gpresult` evidence.
- Effective membership evidence.
- Change-record approval and test-server result.

## GPO-Servers-PAM-RemoteSAM

### Required configuration

| Setting | Required value |
|---|---|
| Network access setting | Restrict clients allowed to make remote calls to SAM |
| Principal | `Server-PAM-ScanningAccount` |
| Permission | Allow |

Remote SAM is required to support approved Delinea account discovery and validation where Remote SAM access is not otherwise available.

### SDDL handling

Do not generate or present an SDDL value unless an approved source supplies it. A policy update must not accidentally overwrite existing SDDL permissions that other approved applications rely on.

### Validation

1. Capture the existing effective Remote SAM setting and SDDL before change.
2. Apply the GPO to an approved test server.
3. Confirm policy precedence and effective settings.
4. Validate a remote SAM request only from an approved Discovery Engine source.
5. Confirm non-approved source calls remain denied.

### Rollback

Restore the prior Remote SAM setting and SDDL evidence. Reapply policy and validate existing administrative services are unaffected.

## GPO-Servers-PAM-RPCFirewall

### Confirmed matrix

| Function | Protocol | Supplied port | Scope requirement |
|---|---|---|---|
| RPC Endpoint Mapper | TCP | 135 | Approved Discovery Engine IPs only |
| SMB / Microsoft-DS | TCP/UDP | 445 | Approved Discovery Engine IPs only |
| Dynamic RPC | TCP/UDP | 49152-65535 | Approved Discovery Engine IPs only |
| NetBIOS discovery | UDP | 137-138 | Approved Discovery Engine IPs only |
| WinNT ADSI provider | TCP | 139 | Approved Discovery Engine IPs only |

**Policy:** Domain profile, Allow action, restricted to approved Discovery Engine IP sources.

### TBC validation items

> [!IMPORTANT]
> TBC: UDP 445 is supplied in the matrix but must be validated against Windows and Delinea requirements.
> Owner: Network and PAM teams

> [!IMPORTANT]
> TBC: UDP dynamic RPC requirement and exact RPC range must be validated; TCP/UDP direction and host-firewall implementation need approval.
> Owner: Windows, network, and PAM teams

> [!IMPORTANT]
> TBC: NetBIOS 137-139 requirements and whether 139 is host, network, or both require validation.
> Owner: Network and Windows teams

Do not configure an unrestricted remote scope.

## Policy conflict and rollback controls

- Record existing firewall profiles and rules before implementation.
- Use the least permissive approved source scope.
- Test on VCCNET and VCCMFG representatives if implementation differences exist.
- Validate that Domain-profile rules do not conflict with Higher-precedence rules.
- Roll back to the exact prior rule set and evidence.

## Evidence checklist

- GPO name and GUID or export.
- OU link and security filtering.
- Policy conflict review.
- Effective policy output.
- Firewall rule export restricted to the change scope.
- Remote SAM validation output.
- Test-server and production-server evidence.

## Source and validation status

**Confirmed:** Target OU, identities, groups, GPO names, ScannerAccess settings, Remote SAM principal, and the supplied firewall matrix.  
**TBC:** Exact SDDL, RPC range implementation, traffic direction, host/network split, security filtering details in non-production, and hostname-to-IP mappings.
