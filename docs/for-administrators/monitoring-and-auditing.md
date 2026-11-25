# Monitoring and Auditing

**Purpose:** Define audit, monitoring, and evidence expectations for PAM 2.0.  
**Audience:** Security operations, PAM operations, auditors, and incident managers.

## Required audit domains

The approved design requires audit coverage for:

- Discovery and onboarding.
- Credential configuration and verification.
- Password rotation.
- Governed checkout and retrieval.
- Entra ID SSO and MFA events.
- Cyolo session authorization and session lifecycle.
- Historical-password access.
- LAPS exclusion and effective policy evidence.
- Snapshot-recovery approval and reconciliation.

## Audit ownership

| Activity | Primary audit owner |
|---|---|
| Credential generation, storage, rotation, history, and checkout | Delinea Secret Server |
| Identity and MFA | Microsoft Entra ID |
| Session launch | Cyolo Session Manager |
| Server policy and account state | Windows and Active Directory |
| Discovery | Delinea Discovery Engine |

## Monitoring requirements

> [!IMPORTANT]
> TBC: SIEM destination, event retention, alert rules, health metrics, and on-call alert routing.
> Owner: Security operations and PAM operations

At minimum, the operations process should detect:

- LAPS and Delinea ownership conflict.
- Delinea heartbeat failure.
- Credential verification failure.
- Unexpected rotation failure.
- Unauthorized or unusual checkout.
- Historical-password access outside an approved recovery request.
- Session launch failure or unexpected target.
- Account lockout or disablement.
- Discovery engine connectivity failure.

## Evidence standards

Record:

- Timestamp and timezone.
- Server or system identifier.
- Change or incident reference.
- Actor or authorized role.
- Event status.
- Rotation or recovery status.
- Verification status.
- Audit event references.

Do not record password values, tokens, or sensitive screenshots.

## Historical-password access monitoring

Historical-password access must be associated with:

- A valid incident or change.
- An authorized recovery role.
- The snapshot and restoration timestamps.
- The password version or timestamp reference, without the password value.

Standard end users must not have access to password history.

## Audit validation runbook

### Purpose

Confirm that an access or lifecycle event creates the required audit evidence.

### Trigger

- New onboarding.
- Scheduled validation.
- Incident or security investigation.
- Post-change quality review.

### Required role

- PAM operator.
- Security operations analyst.
- Cyolo or Entra ID administrator for relevant event validation.

### Procedure

1. Identify the change or incident reference.
2. Capture the start time and timezone.
3. Review Delinea lifecycle events.
4. Review Entra ID identity and MFA events.
5. Review Cyolo session events.
6. Review Windows or AD policy evidence where relevant.
7. Check that no credential value is exposed in logs or ticket evidence.
8. Record missing or conflicting events.
9. Escalate unresolved audit gaps.

### Validation

- Every high-risk action has an audit trail.
- Actor and target are identifiable.
- The incident or change reference is present.
- Password values are not visible in evidence.
- Historical-password access is restricted and complete.

### Evidence

- Event timestamps and event identifiers.
- Change or incident reference.
- Actor and target identifiers.
- Audit system and source location.
- Validation result.

### Rollback

Audit monitoring configuration is rolled back only by the change owner. Restore the prior approved logging or retention setting and revalidate source events.

### Stop conditions

- Credential values are visible in logs or evidence.
- Historical-password access lacks an approved role or ticket.
- Required source events are unavailable.
- Audit timestamps conflict without explanation.

### Escalation

Escalate audit gaps to the PAM operations team and security operations. Escalate uncontrolled credential exposure to the incident process immediately.

## Open decisions

> [!IMPORTANT]
> TBC: Audit retention period, SIEM destination, alert severity, and security operations response targets.
> Owner: Security operations and service owners
