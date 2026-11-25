# Frequently Asked Questions

**Purpose:** Answer common end-user questions about the Windows breakglass account password workflow.  
**Audience:** End users.

## What is breakglass access?

Breakglass access is controlled, exceptional access used when standard permissions are unavailable or insufficient for an approved emergency or change.

## When should I use it?

Use breakglass access only when normal access is unavailable or cannot complete the approved task. It must be supported by a valid incident, request, or change.

## Do I need MFA?

Yes. Sign in to Delinea and Cyolo using the required corporate authentication and MFA.

## Do I need a ticket reference?

Yes. Provide an incident, request, or change reference and a clear justification.

## Which portals do I use?

- **Delinea Secret Server:** https://pam.volvocars.net/secretserver/login.aspx?preventautologin=true
- **Cyolo:** https://login.volvocars.cyolo.io/welcome

## How do I retrieve the Windows breakglass password?

Open Delinea Secret Server, locate the authorized Windows host and breakglass account, enter the required justification, and select **Check Out Password**.

## How long is the password valid?

The checked-out password remains valid for up to 8 hours. Check it in promptly after completing the work.

## How do I connect to the target?

Sign in to Cyolo, select the authorized target, launch the secure session, and authenticate using the password retrieved from Delinea.

## What happens after I finish?

Close the secure session, update the incident, request, or change with the outcome and relevant evidence, and check in the password in Delinea.

## What if the server was restored from a snapshot?

Do not attempt password recovery or repeated sign-in attempts. Stop and contact the PAM support team.

## What if I cannot access the target?

Check that you selected the correct authorized target and completed SSO and MFA. If the problem continues, stop and contact PAM support. Do not bypass the workflow or use undocumented credentials.

## Can I share or store the password?

No. Passwords must not be shared, exported, recorded, or stored outside approved systems.

## Where do I get support?

Use the [Getting Help](getting-help.md) page for the PAM email, ServiceNow request process, incident queue, escalation routine, and contact list.
