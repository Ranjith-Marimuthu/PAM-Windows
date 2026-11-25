# Breakglass User Handbook

**Purpose:** Describe the basic responsibilities and usage rules for authorized breakglass access.  
**Audience:** End users.

## Prerequisites

- The target must be authorized for your request.
- Your incident, request, or change must be active and valid.
- You must be eligible for breakglass access.
- You must be able to complete corporate SSO and MFA.

## Sign in

1. Open the approved PAM access portal.
2. Sign in using Microsoft Entra ID SSO.
3. Complete the required MFA challenge.
4. Confirm that you are signing in with the correct corporate identity.

> [!IMPORTANT]
> TBC: The PAM access portal URL has not been supplied.
> Owner: PAM platform team

## Find an authorized target

1. Search or browse for the target associated with your approved request.
2. Confirm the target name and environment before requesting access.
3. Stop and request help if the target is not authorized or its purpose is unclear.

## Provide justification

Enter a clear, specific justification and provide the incident, request, or change reference. Use a short description that explains:

- Why breakglass access is required.
- The task you need to perform.
- The approved scope and expected duration.

Do not provide sensitive credentials or unnecessary personal data in free-text justification fields.

## Launch a secure session

1. Complete either immediate emergency access or approval-based access, as applicable.
2. Open the authorized target through the secure session mechanism.
3. Use the session only for the approved task.
4. Close the session when the task is complete or when access is no longer required.

## User responsibilities

- Use the minimum access and time necessary.
- Follow the incident, request, or change plan.
- Do not share, export, or record credentials.
- Do not alter unrelated services or configurations.
- Do not attempt snapshot recovery.
- Report unexpected behavior or session problems immediately.
- Update the related ticket with the work performed and outcome.

For a VM restored from an older snapshot, contact the PAM support team. Do not attempt credential recovery yourself.

## Source and validation status

**Confirmed:** SSO, MFA, authorized target selection, justification, ticket reference, secure Cyolo session launch, and ticket closure are required.  
**TBC:** Portal location and exact user interface labels.
