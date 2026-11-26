# Troubleshooting

**Purpose:** Provide a safe decision sequence for PAM 2.0 breakglass access and credential problems.  
**Audience:** PAM operators, Windows engineers, identity engineers, network engineers, and incident responders.

## Troubleshooting sequence

1. Confirm the incident or change scope.
2. Confirm the exact target identity and environment.
3. Exclude identity and MFA issues.
4. Exclude approval or eligibility issues.
5. Exclude network, routing, and firewall issues.
6. Exclude account lockout or disablement.
7. Exclude username or domain format issues.
8. Confirm Delinea heartbeat and credential state.
9. Confirm Cyolo target and session state.
10. Confirm LAPS exclusion.
11. Check for snapshot restoration.
12. Review audit events.

## Failure matrix

| Symptom | Likely checks | Stop condition |
|---|---|---|
| SSO or MFA fails | Entra ID status, identity state, MFA result | Repeated authentication attempts after lockout risk |
| User not eligible | Approval and eligibility groups | Group membership or approval policy is unresolved |
| Target not found | Target enrollment, OU, security filtering, Cyolo mapping | Target identity or mapping is uncertain |
| Session cannot launch | Cyolo target mapping, network path, firewall, account state | Snapshot mismatch or credential state unknown |
| Heartbeat fails | Network path, GPO, account lockout, credential mismatch | LAPS exclusion is not verified |
| Rotation fails | LAPS conflict, account state, password changer, network | Any simultaneous ownership is suspected |
| Authentication fails | Username format, lockout, snapshot, credential state | Stop before repeated attempts |
| Account disabled or locked | AD account state, lockout threshold, approved unlock process | Lockout threshold or recovery role is unknown |
| Discovery missing | Engine assignment, network scope, GPO, Remote SAM | Hostname-to-IP mapping is unverified |

## SSO and MFA

1. Confirm the user identity and MFA completion.
2. Review Entra ID events.
3. Confirm the user is entitled to the PAM application.
4. Do not bypass MFA or share approval.
5. Escalate identity issues to the IAM or support team.

For support channels and escalation contacts, see [Getting Help](../for-end-users/getting-help.md).

## Approval and eligibility

> [!IMPORTANT]
> Eligibility groups, approvers, approval routing, and timed-access duration must be confirmed with PAM governance and IAM teams.

Do not grant access through a manual workaround while approval policy is unresolved.

## Network and discovery

1. Confirm the assigned Discovery Engine and source IP.
2. Confirm hostname-to-IP mapping through DNS, CMDB, or IPAM.
3. Confirm approved ports and source restriction.
4. Confirm Domain profile firewall policy.
5. Confirm Remote SAM and local membership.
6. Stop if an unrestricted rule or unknown source is required.

## Account lockout

> [!IMPORTANT]
> Confirm the lockout threshold and approved unlock process with Windows infrastructure and AD teams before attempting further authentication.

Before more authentication attempts:

1. Confirm account lockout state.
2. Stop repeated credential tests.
3. Confirm whether VM snapshot mismatch may be present.
4. Use the approved recovery or incident process. For support channels and escalation, see [Getting Help](../for-end-users/getting-help.md).

## LAPS conflict

Check for:

- LAPS policy still targeting the server.
- LAPS exclusion not effective.
- A previous LAPS rotation state.
- Manual or undocumented credential reset.

If simultaneous ownership is suspected:

1. Stop Delinea rotation.
2. Preserve evidence.
3. Review the [Active Directory and GPO requirements](PAM-Windows-GPO-Requirements.md).
4. Escalate to Windows and PAM teams using the [Getting Help](../for-end-users/getting-help.md) support process.

## Snapshot mismatch

If the VM may have been restored from an older snapshot:

1. Stop normal authentication attempts.
2. Record snapshot and restoration timestamps.
3. Confirm timezone.
4. Exclude unrelated network and account issues.
5. Do not attempt password history access without an authorized recovery role.
6. Contact PAM support through the process described in [Getting Help](../for-end-users/getting-help.md).

## Cyolo session issues

1. Confirm Entra ID SSO and MFA.
2. Confirm approval and eligibility.
3. Confirm the target mapping.
4. Confirm network connectivity.
5. Confirm account state.
6. Confirm Delinea credential state separately.
7. Launch only one controlled test session.

Do not disable MFA or approval controls to restore a session.

## Audit gaps

1. Identify the event type and time range.
2. Confirm the change or incident reference.
3. Compare Delinea, Entra ID, Cyolo, and Windows evidence.
4. Confirm credential values are not exposed.
5. Escalate missing source events to security operations.

## Offboarding

### Purpose

Remove a Windows server or authorized identity safely from the PAM 2.0 process.

### Trigger

- Server decommission or environment migration.
- User or approver offboarding.
- Target no longer authorized.
- Change or incident requires removal.

### Required role

- PAM administrator.
- Windows administrator.
- AD administrator.
- Change approver.

### Procedure

1. Confirm decommission or offboarding approval.
2. Confirm active sessions and checkouts are closed or expired.
3. Remove or defer the server from discovery scope.
4. Remove production target group membership if no longer approved.
5. Remove or retire the three PAM GPO applications as appropriate.
6. Remove Cyolo target access.
7. Remove PAM eligibility and approval access.
8. Remove or retain the Delinea secret according to the approved decommission policy.
9. Confirm no LAPS conflict remains where applicable.
10. Preserve audit and decommission evidence.

### Validation

- Server or identity is no longer authorized.
- Active checkout and sessions are closed or unavailable.
- GPO and target scope no longer apply.
- Audit events record the offboarding.

### Evidence

- Decommission or offboarding approval.
- Server or identity identifier.
- GPO and target membership evidence.
- Delinea and Cyolo removal evidence.
- Audit event references.

### Rollback

Restore access only through an approved change and only if the server or identity is still validly in scope.

### Stop conditions

- Server is still in use or not formally decommissioned.
- Active incident or approved session still requires access.
- Decommission record conflicts with ownership records.

### Escalation

Escalate decommission or access conflicts to the PAM operations, infrastructure, IAM, and change teams. For support channels and escalation contacts, see [Getting Help](../for-end-users/getting-help.md).
