# Source Register

**Purpose:** Record the source hierarchy and validation status used in this repository.  
**Audience:** Authors, reviewers, auditors, and change approvers.

## Source hierarchy

1. Requirements in the controlled meta-prompt.
2. Approved architecture and implementation documents.
3. Existing GitHub Markdown files.
4. PAM artifacts and supplied process diagrams.
5. Emails, chats, meetings, and transcripts.
6. Delinea Secret Server vendor documentation.

Informal conversations are not approved design decisions.

## Register

| Source | Status | Used for | Approval needed |
|---|---|---|---|
| Controlled meta-prompt supplied for PAM 2.0 | Confirmed | Scope, component responsibilities, infrastructure facts, GPO requirements, workflows, security rules | No; used as the explicit approved requirements source |
| PAM artifacts and process diagram | TBC/not supplied in workspace | Implementation details and diagram evidence | Supply approved artifact or diagram |
| Approved architecture document | TBC/not supplied | Production topology and implementation status | Supply and record approval |
| Delinea Secret Server v12 documentation | TBC/not supplied | Vendor configuration verification | Review only through approved product reference |
| AD/Group Policy evidence | TBC/not supplied | SDDL, effective policy, exact LAPS method | Supply approved implementation evidence |
| Network/firewall evidence | TBC/not supplied | Traffic direction, exact protocols, host/network ownership | Supply approved rule and design evidence |
| Discovery engine DNS/CMDB/IPAM evidence | TBC/not supplied | Hostname-to-IP mapping | Supply validated evidence |
| Support and process records | TBC/not supplied | Support, escalation, approvals, retention | Supply approved service record |

## Label definitions

- **Confirmed:** Explicitly supported by an approved source.
- **Planned:** Approved but not confirmed as implemented.
- **TBC:** Missing or conflicting information.

## Source review actions

1. Replace TBC items with evidence when approved sources become available.
2. Update all affected pages and the open decisions register.
3. Add a source identifier and reviewer approval to configuration changes.
4. Do not copy large vendor sections; summarize and link to approved vendor references.

## Source and validation status

**Confirmed:** Source hierarchy and the confirmed facts identified in the controlled requirements.  
**TBC:** Approved architecture documents, PAM artifacts, process diagrams, configuration evidence, and operational contacts were not supplied in the workspace.
