# Getting Help

**Purpose:** Guide users to the appropriate support path for breakglass access problems.  
**Audience:** End users.

## Before contacting support

Have this information ready:

- The active incident, request, or change reference.
- The target name and environment.
- A description of the access or session problem.
- The approximate time of the issue.
- Any error message shown, with no credential values.

Do not include passwords or sensitive session information in tickets or email.

## Access support situations

### Sign-in or MFA problems

If SSO or MFA fails:

1. Stop repeated sign-in attempts.
2. Confirm the active corporate identity.
3. Record the error shown.
4. Contact normal identity or PAM support for assistance.

### Target not found or unauthorized

Check that you are in the correct environment and that the target belongs to the approved request. If it is missing or unauthorized, update the ticket and contact PAM support.

### Access waiting for approval

If access is approval-based:

1. Verify that the request was submitted.
2. Confirm the approver and reference.
3. Do not use alternative access methods.
4. Contact support only if the approved deadline is at risk.

### VM snapshot recovery

If a VM may have been restored from an older snapshot:

1. Stop standard sign-in attempts.
2. Do not perform credential-recovery actions.
3. Contact the PAM support team and provide the incident or change reference.

Snapshot recovery is restricted to authorized PAM administrators.

## Escalation information

> [!IMPORTANT]
> TBC: PAM support email, ServiceNow category, escalation hours, on-call process, and support team contacts.
> Owner: PAM operations and service management

## User safety rules

- Never copy credentials into tickets, email, chat, or files.
- Never share an active session or approval.
- Never attempt undocumented password recovery.
- Never disable security controls to regain access.
- Use the support process for all unresolved access problems.

## Source and validation status

**Confirmed:** VM snapshot recovery must be escalated to the PAM support team.  
**TBC:** Support channels, escalation contacts, and service levels.
