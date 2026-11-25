# PAM 2.0: Windows Breakglass Password Management

**Purpose:** Provide an entry point for end-user and administrator documentation.  
**Audience:** Authorized users, PAM administrators, infrastructure teams, and auditors.

## Documentation sections

- [End-User Documentation](for-end-users/index.md)
- [Administrator Documentation](for-administrators/index.md)
- [Glossary](glossary.md)
- [Open Decisions](open-decisions.md)
- [Reference Documentation](reference/configuration-matrix.md)

## Scope

This documentation describes management of the Windows local breakglass account `volvop27` for approved VCCNET and VCCMFG servers using Delinea Secret Server, Delinea Discovery Engines, Active Directory and Group Policy, Microsoft Entra ID, and Cyolo Session Manager.

Delinea replaces LAPS for `volvop27`. Delinea owns password generation, storage, rotation, verification, history, governed retrieval, and audit. Cyolo provides controlled target connectivity without owning or rotating the credential.

## Access boundary

End users should use the [End-User Resources](for-end-users/index.md). Administrators must use the [Administrator Resources](for-administrators/index.md) for architecture, GPO, network, onboarding, password, recovery, and audit procedures.

## Source and validation status

**Confirmed:** Account ownership, role separation, target scope, and documented component responsibilities.  
**Planned:** Entra ID, Cyolo, GPO, and Delinea implementation items not otherwise marked as implemented.  
**TBC:** Configuration values, approvals, integration methods, support contacts, and some network mappings.
