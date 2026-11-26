# RACI Matrix

**Purpose:** Define accountability boundaries for PAM 2.0 implementation and operations.  
**Audience:** PAM , infrastructure, IAM, network, security, and service owners.

Legend: **R** Responsible, **A** Accountable, **C** Consulted, **I** Informed.

| Activity | PAM Team | Windows infrastructure | AD/GPO | Network | IAM/Entra ID | Cyolo | Security operations | Change manager |
|---|---|---|---|---|---|---|---|---|
| Architecture  | A/R | C | C | C | C | C | C | I |
| Delinea configuration | A/R | C | I | C | C | C | C | I |
| Account onboarding | R | R | C | C | I | C | I | C |
| LAPS exclusion | C | A/R | R | I | I | I | C | C |
| Rotation enablement | A/R | C | C | I | I | I | C | C |
| GPO implementation | C | R | A/R | C | I | I | C | C |
| Network firewall implementation | C | C | I | A/R | I | C | C | C |
| Discovery and connectivity | A/R | C | C | R | I | I | C | C |
| Entra ID SSO/MFA | C | I | I | I | A/R | C | C | I |
| Cyolo session integration | C | C | I | C | C | A/R | C | C |
| Snapshot recovery | A/R | R | C | C | C | C | C | A |
| Audit and monitoring | R | C | C | C | C | C | A/R | I |
| Troubleshooting | R | R | R | R | R | R | C | C |
| Offboarding | R | R | R | C | R | R | C | C |


