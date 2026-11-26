# Windows Breakglass PAM Operations Runbook

## Purpose

This runbook provides the PAM Operations team with standard procedures to monitor, validate, and troubleshoot Windows breakglass accounts managed in Delinea Secret Server.

## Scope

This runbook covers:

- Windows assets onboarded to Delinea Secret Server.
- The Windows breakglass account `vorlvop27`.
- Delinea Discovery, Heartbeat, password rotation, and reconciliation.
- Credential checkout and Cyolo session access.
- Escalation to Windows, Network, IAM, or Cyolo support teams.

## Important Controls

> [!IMPORTANT]
> - Do not expose, copy, or record the breakglass password in a ticket, email, chat, or evidence file.
> - Do not manually reset or reconcile a password without an approved incident or change record.
> - Do not enable, unlock, or modify the account directly unless the action is approved.
> - Confirm that `vorlvop27` is excluded from LAPS before making credential changes.
> - Stop troubleshooting if both LAPS and Delinea appear to manage the account.
> - Record all actions and results in the associated incident or change record.

## Roles and Responsibilities

| Team | Responsibility |
|---|---|
| PAM Operations | Delinea asset, secret, Heartbeat, password rotation, reconciliation, checkout, and audit checks |
| Windows Operations | Windows server availability, local account state, GPO application, and operating system issues |
| Network Operations | Routing, firewall, RPC, and SMB connectivity |
| IAM Operations | Entra ID, SSO, MFA, and identity-related failures |
| Cyolo Operations | Cyolo authorization, target mapping, connector, and session issues |

---

# Runbook 1: Validate Breakglass Target Health

## Use This Runbook When

- Performing a scheduled health check.
- Validating a newly onboarded server.
- Validating service after a change.
- Investigating a general breakglass access complaint.
- Confirming recovery after an incident.

## Required Information

Before starting, obtain:

- Incident, request, or change reference.
- Target server name.
- Environment, such as production or non-production.
- Delinea asset and secret name.
- A PAM-approved test identity, if access testing is required.

## Procedure

1. Sign in to Delinea Secret Server using the approved PAM Operations role.
2. Search for the target Windows server.
3. Confirm that the asset is active and located in the correct Windows folder.
4. Confirm that the `vorlvop27` secret is linked to the correct asset.
5. Confirm that the secret is enabled for PAM management.
6. Review the latest Discovery result.
7. Review the latest Heartbeat result.
8. Review the last successful password change.
9. Check for pending or failed password-change jobs.
10. Confirm that no unresolved reconciliation error exists.
11. Review recent audit events for the asset and secret.
12. If approved, perform one controlled checkout or Cyolo session test.
13. Record the results in the incident or change record.

## Expected Results

| Check | Expected Result |
|---|---|
| Delinea asset | Present and active |
| Folder placement | Correct Windows folder |
| Breakglass secret | `vorlvop27` linked to the correct asset |
| Discovery | Successful |
| Heartbeat | Successful |
| Password management | Enabled |
| Password-change job | No unresolved failure |
| Reconciliation | No unresolved error |
| Checkout or Cyolo test | Successful, if tested |
| Audit events | Available |

## If a Check Fails

| Failure | Next Action |
|---|---|
| Asset is missing | Use the discovery and onboarding runbook |
| Secret is missing or incorrectly linked | Escalate to a Delinea administrator |
| Heartbeat fails | Use Runbook 2 |
| Password rotation fails | Review the password-change job and reconciliation status |
| Checkout fails but Heartbeat succeeds | Check secret permissions and access approval |
| Cyolo session fails but checkout succeeds | Use Runbook 3 |
| Server is unavailable | Escalate to Windows Operations |
| Network connectivity fails | Escalate to Network Operations |

## Completion Criteria

Close the operational task when:

- The asset and secret are correctly linked.
- Discovery and Heartbeat succeed.
- No unresolved password-change or reconciliation error exists.
- Approved checkout or session testing succeeds, if required.
- Audit evidence and the operational record are updated.

---

# Runbook 2: Investigate a Heartbeat Failure

## Use This Runbook When

- Delinea reports a Heartbeat failure.
- Password verification fails.
- Password rotation fails.
- A credential mismatch is suspected.
- The breakglass account is reported as locked or disabled.

## Procedure

### 1. Confirm the Failure

1. Open the `vorlvop27` secret in Delinea Secret Server.
2. Record the latest Heartbeat status and timestamp.
3. Record the displayed error message or error code.
4. Check whether the issue affects:
   - One server.
   - Multiple servers.
   - All servers using the same Discovery Engine.
5. Review the last successful Heartbeat and password change.

### 2. Check the Delinea Configuration

Confirm that:

- The secret is active.
- The secret is linked to the correct Windows asset.
- The correct password changer is assigned.
- The assigned Discovery Engine or engine site is available.
- No password-change or reconciliation job is stuck.
- The secret has not been moved to an incorrect folder or policy.
- The `vorlvop27` account is not being managed by both LAPS and Delinea.

### 3. Check Target Connectivity

From an approved administrative source, test the required connectivity:

```powershell
Test-NetConnection -ComputerName <ServerName> -Port 445
Test-NetConnection -ComputerName <ServerName> -Port 135
```

Expected result:

```text
TcpTestSucceeded : True
```

> [!NOTE]
> Dynamic RPC connectivity can use TCP ports `49152-65535`. Network Operations should validate the effective firewall path when TCP 135 succeeds but the remote operation still fails.

### 4. Request Windows Account Validation

Ask Windows Operations to confirm that:

- `vorlvop27` exists on the target server.
- The account is enabled.
- The account is not locked.
- The account is a member of the required local group.
- The PAM GPOs are applied.
- No LAPS policy is managing the same account.

Windows Operations can validate the local account with:

```powershell
Get-LocalUser -Name "vorlvop27"
```

GPO application can be checked with:

```cmd
gpresult /h C:\Windows\Temp\pam-gpresult.html
```

> [!IMPORTANT]
> PAM Operations must not request that Windows Operations manually set a new password unless an approved reconciliation or recovery procedure is being followed.

### 5. Retry Heartbeat

After the identified issue has been corrected:

1. Run one Heartbeat from Delinea.
2. Confirm that the Heartbeat succeeds.
3. Perform an approved checkout test if required.
4. Review the resulting audit events.
5. Attach the non-sensitive evidence to the incident record.

## Common Failures

| Symptom | Likely Cause | Action |
|---|---|---|
| Target cannot be reached | Server, DNS, routing, or firewall issue | Escalate to Windows or Network Operations |
| Access denied | Account permissions, GPO, or remote access restriction | Escalate to Windows Operations |
| Account does not exist | Incorrect target or account not provisioned | Validate onboarding and server build |
| Account disabled or locked | Windows account state | Request approved correction from Windows Operations |
| Password mismatch | Credential changed outside Delinea or restored snapshot | Stop normal testing and follow reconciliation or snapshot recovery |
| Heartbeat works on other servers only | Target-specific Windows or firewall issue | Escalate with target evidence |
| Multiple targets fail on one engine | Discovery Engine or network-path issue | Escalate to the PAM platform and Network teams |
| LAPS and Delinea both manage the account | Ownership conflict | Stop changes and escalate to PAM and Windows service owners |

## Stop Conditions

Stop troubleshooting and escalate when:

- The active password is unknown.
- A password mismatch is confirmed.
- LAPS exclusion cannot be confirmed.
- Both LAPS and Delinea appear to manage `vorlvop27`.
- An older virtual-machine snapshot may have been restored.
- Manual password modification is required.
- Repeated testing could lock the account.
- The required network or GPO scope is unknown.

## Completion Criteria

The incident can be resolved when:

- Heartbeat succeeds.
- The account is managed only by Delinea.
- No unresolved password-change or reconciliation failure remains.
- An approved checkout test succeeds, if required.
- The cause, correction, and evidence are recorded.

---

# Runbook 3: Investigate a Password Rotation Failure

## Use This Runbook When

- A scheduled password change fails.
- Delinea reports that the password is out of sync.
- Heartbeat succeeds but password rotation fails.
- A reconciliation job is pending or unsuccessful.

## Procedure

1. Open the affected secret in Delinea.
2. Record the password-change error and timestamp.
3. Confirm the correct Windows password changer is assigned.
4. Confirm the asset mapping and account name.
5. Check the Heartbeat result.
6. Review the password history metadata without displaying password values.
7. Check whether another process changed the account password.
8. Confirm that LAPS does not manage `vorlvop27`.
9. Confirm that the target server was not restored from an older snapshot.
10. If the credential state is known and the action is approved, retry the password change once.
11. If the credential state is unknown, stop and use the approved reconciliation process.
12. Run Heartbeat after the password change or reconciliation.
13. Record the result in the incident or change record.

## Completion Criteria

- Password rotation succeeds.
- Heartbeat succeeds using the current managed credential.
- No unresolved reconciliation job remains.
- The result is recorded without exposing the password.

## Escalation

Escalate to the Delinea administrator and Windows Operations if:

- Reconciliation fails.
- The active credential is unknown.
- The account is locked or disabled.
- A snapshot restore is suspected.
- LAPS ownership is unclear.
- Password rotation repeatedly fails.

---

# Runbook 4: Investigate a Cyolo Session Failure

## Use This Runbook When

- A Cyolo session does not launch.
- MFA or SSO fails.
- The target is unavailable or unauthorized.
- A session terminates unexpectedly.
- Windows authentication fails during session launch.

## Procedure

### 1. Identify the Failure Layer

Confirm whether the failure occurs during:

1. Entra ID authentication.
2. MFA.
3. Cyolo authorization.
4. Cyolo target selection.
5. Connection to the Windows server.
6. Windows account authentication.

### 2. Check PAM Health

In Delinea Secret Server:

1. Confirm that the asset and `vorlvop27` secret are active.
2. Confirm that the latest Heartbeat succeeds.
3. Confirm that no password-change or reconciliation error exists.
4. Confirm that the requesting user has the required Delinea permissions.
5. Review the relevant audit events.

### 3. Check Cyolo Access

Confirm that:

- The user is assigned to the correct Cyolo access policy.
- The target server is mapped correctly.
- The relevant Cyolo connector is available.
- The user has approval for the requested target and access period.

### 4. Perform One Controlled Test

If identity, authorization, PAM health, and target connectivity are confirmed:

1. Launch one controlled test session.
2. Confirm that the intended target is opened.
3. Confirm that the credential is injected without being exposed.
4. Confirm that Delinea and Cyolo audit events are generated.

## Failure Routing

| Failure Point | Escalate To |
|---|---|
| Entra ID or MFA | IAM Operations |
| Cyolo policy or authorization | Cyolo Operations |
| Cyolo target mapping or connector | Cyolo Operations |
| Delinea Heartbeat or credential | PAM Operations or Delinea administrator |
| Windows account or RDP | Windows Operations |
| Routing or firewall | Network Operations |

## Stop Conditions

Stop testing when:

- User identity or MFA cannot be validated.
- The user does not have approved target access.
- The managed credential state is unknown.
- A password mismatch is suspected.
- A snapshot restore is suspected.
- Testing could expose a credential or bypass approval controls.

## Completion Criteria

- SSO and MFA succeed.
- Cyolo authorization is correct.
- The Delinea Heartbeat succeeds.
- The session connects to the intended Windows server.
- The credential is not exposed.
- Audit events are available.

---

# Runbook 5: Validate a Newly Onboarded Windows Server

## Use This Runbook When

A Windows server has been automatically onboarded through Delinea Discovery.

## Procedure

1. Search for the server in Delinea Secret Server.
2. Confirm that the asset is in the approved Windows folder.
3. Confirm that the discovered account is `vorlvop27`.
4. Confirm that the secret is linked to the correct server.
5. Confirm the correct secret template and password changer.
6. Confirm the expected Infra Team access permissions.
7. Run Heartbeat.
8. Confirm password management is enabled according to the onboarding design.
9. Review the Discovery and audit events.
10. Record the onboarding result.

## Completion Criteria

| Check | Expected Result |
|---|---|
| Asset | Created in the approved Windows folder |
| Account | `vorlvop27` discovered |
| Secret mapping | Linked to the correct Windows server |
| Permissions | Approved Infra Team access assigned |
| Heartbeat | Successful |
| Password management | Enabled |
| Audit | Discovery and onboarding events available |

---

# Daily PAM Operations Checklist

| Check | Expected Action |
|---|---|
| Discovery job failures | Review and assign for investigation |
| Newly discovered assets | Confirm onboarding and folder placement |
| Heartbeat failures | Investigate using Runbook 2 |
| Password-change failures | Investigate using Runbook 3 |
| Reconciliation failures | Review and escalate if the credential state is unknown |
| Cyolo session failures | Identify the failure layer and route to the responsible team |
| Stale or unmanaged assets | Validate ownership and onboarding status |
| Repeated failures | Open or update a problem record |
| Audit events | Confirm that operational events are available |

---

# Evidence Checklist

Record the following without including credential values:

- Incident, request, or change number.
- Target server name.
- Delinea asset and secret names.
- Failure timestamp.
- Heartbeat status and timestamp.
- Discovery status.
- Password-change or reconciliation status.
- Displayed error message or error code.
- Connectivity test results.
- GPO validation reference, if applicable.
- Cyolo event reference, if applicable.
- Actions performed.
- Final validation result.
- Escalation team and ticket reference.

---

# Escalation Template

```text
Incident/Request:
Target server:
Environment:
Delinea asset:
Secret/account: vorlvop27
Failure type:
Failure timestamp:
Last successful Heartbeat:
Last successful password change:
Displayed error or code:
Discovery Engine/site:
Connectivity result:
GPO status:
LAPS exclusion confirmed: Yes/No
Snapshot restore suspected: Yes/No
Actions completed:
Evidence attached:
Escalation required from:
```
