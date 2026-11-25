# Administrator Resources

**Purpose:** Provide operational, implementation, and recovery documentation for PAM 2.0 Windows breakglass management.  
**Audience:** PAM administrators, Windows infrastructure engineers, AD administrators, network teams, and audit personnel.

## Confirmed scope

The solution manages the Windows local breakglass account `volvop27` on approved VCCNET and VCCMFG servers. Delinea Secret Server owns the credential and its lifecycle; Cyolo provides controlled target connectivity.

Delinea replaces LAPS for `volvop27`. LAPS and Delinea must never manage the account simultaneously.

## Administrator documentation

- [Architecture](architecture.md)
- [Active Directory and GPO](active-directory-and-gpo.md)
- [Network Requirements](network-requirements.md)
- [Discovery and Onboarding](discovery-and-onboarding.md)
- [LAPS to Delinea Transition](laps-to-delinea-transition.md)

## Source and validation status

**Confirmed:** Scope, account ownership, target environments, and the Delinea/Cyolo responsibility boundary are supported by the approved requirements.  
**TBC:** Implemented configuration values, exact integration details, and operational contacts.
