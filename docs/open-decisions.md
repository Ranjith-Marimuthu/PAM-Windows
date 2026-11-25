# Open Decisions

**Purpose:** Record missing or unvalidated design decisions that must be resolved before production implementation.  
**Audience:** PAM architects, administrators, governance, networking, and service owners.

| ID | Decision | Status | Owner | Evidence required |
|---|---|---|---|---|
| OD-01 | Delinea URL, folder, and secret template | TBC | PAM platform team | Approved configuration export |
| OD-02 | Password complexity and rotation policy | TBC | PAM platform team | Approved password policy |
| OD-03 | Heartbeat frequency | TBC | PAM platform team | Approved heartbeat configuration |
| OD-04 | Checkout duration | TBC | PAM governance and IAM | Approved access policy |
| OD-05 | Approval and eligibility groups | TBC | PAM governance and IAM | Entra ID groups and policy mapping |
| OD-06 | Exact LAPS exclusion method | TBC | Windows and AD teams | Validated implementation and evidence |
| OD-07 | Cyolo integration method | TBC | Cyolo and PAM teams | Approved integration design |
| OD-08 | Password-history retention and authorized roles | TBC | PAM governance and audit | Retention policy and role matrix |
| OD-09 | Snapshot-recovery approval model | TBC | PAM governance and change management | Approved approval workflow |
| OD-10 | Credential reconciliation method | TBC | PAM and Windows teams | Validated reconciliation procedure |
| OD-11 | Account lockout threshold | TBC | Windows and AD teams | Approved domain or local policy |
| OD-12 | Audit retention and SIEM destination | TBC | Security operations | SIEM architecture and retention policy |
| OD-13 | WAN outage and offline recovery process | TBC | PAM operations | Approved continuity procedure |
| OD-14 | Discovery schedule and engine assignment | TBC | PAM platform team | Discovery configuration record |
| OD-15 | Hostname-to-IP mapping | TBC | DNS, CMDB, IPAM, network | Validated mapping evidence |
| OD-16 | Support and escalation contacts | TBC | Service management | Support matrix and on-call process |
| OD-17 | Production and non-production differences | TBC | PAM architecture team | Environment topology and configuration matrix |
| OD-18 | UDP 445 and UDP dynamic RPC requirements | TBC | Network and PAM teams | Vendor and implementation validation |
| OD-19 | Exact dynamic RPC range and traffic direction | TBC | Network and Windows teams | Firewall and traffic-flow evidence |
| OD-20 | NetBIOS 137-139 requirement and host/network scope | TBC | Network and Windows teams | Approved traffic requirements |
| OD-21 | Remote SAM SDDL implementation | TBC | AD and Windows teams | Approved policy or SDDL source |

## Decision rules

- Do not implement a TBC item as an assumed configuration.
- Record the approving source and implementation evidence after resolution.
- Update the source register and configuration matrix when a decision is confirmed.
- Stop sensitive implementation if the decision affects credential ownership, access scope, or security controls.

## Source and validation status

**TBC:** All decisions in this register remain unresolved unless an approved source supplies evidence and the relevant page is updated.
