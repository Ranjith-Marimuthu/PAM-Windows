# Operational Runbooks

**Purpose:** Provide common PAM operations runbooks for routine health and controlled response.  
**Audience:** PAM operators, Windows engineers, network engineers, and incident responders.

## Runbook: Validate PAM target health

### Purpose

Confirm that the server, account, discovery path, credential, and session path are operational.

### Trigger

- Scheduled health check.
- Discovery or heartbeat failure.
- Checkout or Cyolo access complaint.
- Change validation.

### Required role

- PAM operator.
- Windows or network engineer for the relevant failure domain.

### Preconditions

- Approved test server and test identity.
- Valid change or health-check reference.
- Effective network and GPO state.

### Procedure

1. Confirm server identity and environment.
2. Confirm account exists and is enabled.
3. Confirm effective LAPS exclusion.
4. Confirm heartbeat and password changer status.
5. Confirm Discovery Engine connectivity.
6. Confirm the authorized network rules.
7. Test governed checkout.
8. Test Cyolo access.
9. Review audit events.

### Validation

- Target is discoverable.
- Account is managed only by Delinea.
- Heartbeat succeeds.
- Checkout and Cyolo access succeed.
- Audit events are available.

### Evidence

- Health-check timestamp.
- Target and account status.
- Discovery, heartbeat, checkout, and session results.
- Audit event references.

### Rollback

No configuration change is made in the standard health check. Revert only temporary test configuration through its original change record.

### Stop conditions

- Account lockout or disablement is present.
- LAPS and Delinea ownership is ambiguous.
- Network route or firewall scope is unknown.
- Credential verification fails.

### Escalation

Escalate to PAM operations, Windows infrastructure, or network operations according to the failed layer.

---

## Runbook: Investigate heartbeat failure

### Purpose

Diagnose whether Delinea can verify `volvop27` on the target.

### Trigger

- Heartbeat failure alert.
- Password verification failure.
- Account lockout or rotation failure.

### Required role

- Delinea administrator.
- Windows infrastructure engineer.
- Network engineer if routing or firewall evidence is required.

### Preconditions

- Target identity and incident reference.
- Delinea heartbeat configuration known.
- Test window and approved recovery role.

### Procedure

1. Confirm the target and server state.
2. Confirm account existence and enablement.
3. Confirm network connectivity from the assigned Discovery Engine or PAM component.
4. Confirm firewall and GPO effective state.
5. Exclude account lockout and disablement.
6. Confirm credential reconciliation status.
7. Confirm no conflicting LAPS process remains active.
8. Verify the credential by the approved method.
9. Record evidence and correct the identified fault.

### Validation

- Heartbeat succeeds.
- No simultaneous LAPS management exists.
- Credential state is reconciled.
- A controlled checkout succeeds.

### Evidence

- Heartbeat logs or status.
- Target and account state.
- Network and GPO evidence.
- Lockout or disablement status.
- Reconciliation result.

### Rollback

Roll back only the configuration changed during diagnosis. Do not restore LAPS ownership while Delinea is active.

### Stop conditions

- Password mismatch or unknown active credential state.
- LAPS exclusion cannot be proven.
- Account lockout threshold or unknown Windows state blocks safe testing.
- Snapshot recovery conditions may apply.

### Escalation

Escalate to PAM operations and Windows infrastructure. Use the snapshot recovery runbook if the server may originate from an older VM snapshot.

---

## Runbook: Investigate Cyolo session failure

### Purpose

Restore a controlled Cyolo session without weakening security controls.

### Trigger

- Session launch failure.
- MFA or SSO failure.
- Target not authorized or not found.
- Unexpected session termination.

### Required role

- Cyolo administrator.
- PAM operator.
- IAM administrator for SSO/MFA.
- Windows or network engineer for target access failures.

### Preconditions

- Incident or change reference.
- Authorized test identity.
- Target and environment confirmed.

### Procedure

1. Confirm the user identity and MFA result.
2. Confirm the target authorization and request scope.
3. Confirm Cyolo target mapping.
4. Confirm network and firewall connectivity.
5. Confirm Windows account state.
6. Confirm Delinea heartbeat and credential verification separately.
7. Relaunch one controlled test session.
8. Confirm audit events.

### Validation

- SSO and MFA work.
- Authorization is correct.
- Cyolo session launches to the intended target.
- No credential value is exposed.

### Evidence

- Entra ID authentication event.
- Cyolo authorization and session event.
- Target and network status.
- Heartbeat and credential state.

### Rollback

Restore only the temporary Cyolo or routing change that caused the failure. Do not bypass MFA or approval controls.

### Stop conditions

- MFA or identity validation is unresolved.
- Target authorization is incorrect.
- Snapshot mismatch is suspected.
- Credential state is unknown.

### Escalation

Escalate to the relevant PAM, identity, Cyolo, or Windows support team.

> [!IMPORTANT]
> TBC: Support contacts, service tiers, alert routing, Cyolo integration details, and offline recovery process.
> Owner: Service owners and operations teams
