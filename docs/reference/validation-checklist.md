# Validation Checklist

**Purpose:** Provide an evidence-oriented checklist for PAM 2.0 implementation and operation.  
**Audience:** Implementers, validators, change managers, auditors, and service owners.

## Pre-implementation

- [ ] Server owner and onboarding approval confirmed.
- [ ] Target is within VCCNET or VCCMFG approved scope.
- [ ] Account `volvop27` exists and is enabled.
- [ ] Server computer object is in `Server-PAM-Prod` if required.
- [ ] Target OU and GPO scope are confirmed.
- [ ] Existing policy conflicts are reviewed.
- [ ] Hostname-to-IP mapping is validated.
- [ ] Network source scope is restricted to approved IPs.
- [ ] TBC configuration items affecting the change are resolved or formally deferred.

## AD and GPO

- [ ] ScannerAccess policy is linked to the approved scope.
- [ ] `Server-PAM-ScanningAccount` has the approved network-right configuration.
- [ ] Built-in Administrators membership uses Update action.
- [ ] Security filtering is correct.
- [ ] Effective `gpresult` evidence is attached.
- [ ] Remote SAM policy has only the approved principal.
- [ ] Existing SDDL was captured and was not overwritten unintentionally.
- [ ] RPC firewall rule is restricted to approved sources.
- [ ] No unrestricted remote scope exists.
- [ ] Unconfirmed protocols and traffic directions are validated.

## Discovery and onboarding

- [ ] Connectivity is successful from the assigned engine.
- [ ] Discovery scan completes for the approved target.
- [ ] `volvop27` is identified correctly.
- [ ] Secret is onboarded using the approved template.
- [ ] Permissions, password changer, heartbeat, and access policy are applied.
- [ ] Current credential is verified.
- [ ] Evidence excludes password values.

## LAPS transition

- [ ] LAPS management state is captured.
- [ ] The exact LAPS exclusion method is validated.
- [ ] Effective LAPS exclusion is proven on the target.
- [ ] No simultaneous LAPS and Delinea ownership exists.
- [ ] Delinea rotation is enabled only after exclusion evidence is complete.
- [ ] Controlled rotation succeeds.
- [ ] New credential heartbeat and authentication succeed.
- [ ] Checkout and Cyolo access succeed.

## Password and access

- [ ] Delinea is the sole password owner.
- [ ] Cyolo does not own or rotate the password.
- [ ] Historical-password access is restricted and audited.
- [ ] Standard users cannot access password history.
- [ ] No password value appears in tickets or evidence.
- [ ] MFA and approval controls are enforced.
- [ ] Audit events are complete.

## Snapshot recovery

- [ ] VM identity is confirmed.
- [ ] Incident or change is valid.
- [ ] Snapshot creation and restoration timestamps are recorded.
- [ ] Timezone is confirmed.
- [ ] Network, Cyolo, username, lockout, and disablement issues are excluded.
- [ ] Password history is available to an authorized role.
- [ ] Matching password version is identified from evidence.
- [ ] No immediately-previous-password assumption was made.
- [ ] Authentication attempts are controlled.
- [ ] Credential state is reconciled.
- [ ] Password is rotated through Delinea.
- [ ] New credential is verified.
- [ ] Checkout and Cyolo access work.
- [ ] Historical password is confirmed inactive.
- [ ] Recovery evidence and audit events are complete.

## Auditing and evidence

- [ ] Actor and target are identifiable.
- [ ] Timestamp and timezone are recorded.
- [ ] Incident or change reference is present.
- [ ] Rotation, checkout, session, and reconciliation events are available.
- [ ] Password values and sensitive screenshots are excluded.
- [ ] SIEM and retention requirements are confirmed once decided.

## Rollback and closure

- [ ] Rollback state is documented before implementation.
- [ ] GPO and firewall changes can be reversed.
- [ ] Delinea rotation can be stopped safely.
- [ ] LAPS is not restored while Delinea remains active unless separately approved.
- [ ] Change record includes test and evidence references.
- [ ] Remaining TBC items are linked to owners.

## Source and validation status

**Confirmed:** Core security gates and validation requirements.  
**TBC:** Any item that depends on unresolved configuration or source evidence.
