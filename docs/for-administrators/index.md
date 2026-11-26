# Administrator Resources

**Purpose:** Provide operational, implementation, and recovery documentation for PAM 2.0 Windows breakglass management.  
**Audience:** PAM administrators, Windows infrastructure engineers, AD administrators, network teams, and audit personnel.

## Confirmed scope

The solution manages the Windows local breakglass account `volvop27` on approved VCCNET and VCCMFG servers. Delinea Secret Server owns the credential and its lifecycle; Cyolo provides controlled target access.

Delinea replaces LAPS for `volvop27`. LAPS and Delinea must never manage the account simultaneously.

## Administrator documentation

- [Infrastructure Architecture](PAM-Architecture.md)
- [Logical Flow](PAM-Windows-Logical-Flow.md)
- [Active Directory and GPO](PAM-Windows-GPO-Requirements.md)
- [Network Topology](PAM-Network-Topology.md)
- [Discovery and Onboarding](PAM-Windows-Discovery-onboarding.md)
- [Password Management](PAM-Windows-Password-management.md)
- [Operational Runbooks](PAM-Windows-Operational-runbooks.md)
- [Troubleshooting](troubleshooting.md)
