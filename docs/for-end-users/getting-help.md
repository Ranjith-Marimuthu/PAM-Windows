# Getting Help

**Purpose:** Guide users to the appropriate support path for Windows breakglass access problems.  
**Audience:** End users.

## Before contacting support

Have this information ready:

- The active incident, request, or change reference.
- The affected CDSID and UNIX server, where applicable.
- The target Windows host and environment.
- A description of the access or session problem.
- The action you were trying to perform.
- The actions already taken, described step by step.
- Whether the server is available.
- Screenshots of error messages, without credential values.

Do not include passwords or sensitive session information in tickets or email.

## PAM support channels

- **PAM support email:** [pam@volvocars.com](mailto:pam@volvocars.com)
- **ServiceNow PAM support request:** https://volvocars.service-now.com/esc?id=sc_cat_item&table=sc_cat_item&sys_id=3cff45f7fb931a9028b5f6efbeefdc7d
- **ServiceNow incident queue:** `PRIV ACCESS MGMT`

## Register an access issue

1. Document a clear description of the problem:
   - Which CDSID is affected and, when relevant, on which UNIX server?
   - What the user is trying to do, for example trying to use `sesu` to access another ID.
   - Describe the problem clearly.
   - Record actions already taken by other teams, step by step.
   - Confirm whether the server is available.
   - Attach a screenshot of the error message or similar evidence if possible.
2. Register the ticket in the **SeOS, PAM** application.
3. Forward the ticket to **PRIV ACCESS MGMT**.

## VM snapshot recovery

If a VM may have been restored from an older snapshot:

1. Stop standard sign-in attempts.
2. Do not perform credential-recovery actions.
3. Contact the PAM support team and provide the incident or change reference.

Snapshot recovery is restricted to authorized PAM administrators.

## High-priority escalation matrix

For high-priority incidents, follow the standard escalation procedures and the appropriate level below.

| Escalation level | Contact name | Phone | Email |
|---|---|---|---|
| PRIV ACCESS MGMT | Sudhakaran Krishnan | (+91) 8778097106 | sudhakaran.krishnan@volvocars.com (primary) |
| PRIV ACCESS MGMT | Tyno Ravindran | (+91) 9495930406 | tyno.raveendran@volvocars.com (secondary) |
| Escalation First level | Varun Golani | (+46) 764318552 | varun.golani@volvocars.com |
| Escalation Second level | Aditya Kucharlapati | (+91) 9920726966 | aditya.kucharlapati@volvocars.com |
| Escalation Third level | Sunil V Palayyan | (+46) 702226236 | sunil.kumar.vimala.palayyan@volvocars.com |

## Ownership and service management

PAM support operations and service escalation are managed by the **PAM operations team and service management**.

## User safety rules

- Never copy credentials into tickets, email, chat, or files.
- Never share an active session or approval.
- Never attempt undocumented password recovery.
- Never disable security controls to regain access.
- Use the support process for unresolved access problems.
