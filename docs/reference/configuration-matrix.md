# Configuration Matrix

**Purpose:** Summarize confirmed PAM 2.0 configuration.  
**Audience:** PAM architects, engineers, auditors, and change approvers.

## Component and responsibility matrix

| Item | Status | Confirmed or unresolved value |
|---|---|---|
| Managed account | Confirmed | `volvop27`, local Windows breakglass account |
| Credential owner | Confirmed | Delinea Secret Server |
| Rotation authority | Confirmed | Delinea Secret Server |
| Password history | Confirmed | Delinea Secret Server |
| Session connectivity | Confirmed | Cyolo Session Manager |
| LAPS | Confirmed constraint | Delinea replaces LAPS; simultaneous management prohibited |
| Entra ID | Planned | SSO and MFA |
| Discovery | Confirmed scope | Delinea Discovery Engines |

## AD and GPO matrix

| Item | Status | Value |
|---|---|---|
| Target OU | Confirmed | `vccnet.volvocars.net/CS/Servers/PROD` |
| Scanning group | Confirmed | `Server-PAM-ScanningAccount` |
| Scanning identity | Confirmed | `BPPPAMWD` |
| Production target group | Confirmed | `Server-PAM-Prod` |
| ScannerAccess GPO | Confirmed | Network logon principal and Administrators Update member |
| RemoteSAM GPO | Confirmed | `Server-PAM-ScanningAccount` Allowed |
| RPCFirewall GPO | Confirmed matrix | Domain profile, Allow, approved source scope |
| Exact SDDL | TBC | Requires approved source |

### Network matrix

| Function | Protocol | Port | Status |
|---|---|---:|---|
| RPC Endpoint Mapper | TCP | 135 | Supplied, validate implementation |
| SMB / Microsoft-DS | TCP/UDP | 445 | Supplied, UDP 445 TBC |
| Dynamic RPC | TCP/UDP | 49152-65535 | Supplied, exact range and UDP TBC |
| NetBIOS discovery | UDP | 137-138 | Supplied, 137-139 scope TBC |
| WinNT ADSI provider | TCP | 139 | Supplied, scope TBC |

## Discovery engine sources
Approved source IPs:

- `10.122.84.93`
- `10.122.84.94`
- `10.122.84.95`
- `10.122.128.87`
- `10.122.128.88`
- `10.46.158.68`
- `10.46.158.69`



