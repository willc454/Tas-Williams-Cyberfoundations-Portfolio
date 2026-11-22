# Executive Summary — Cloud Heights Identity Investigation

> Fictional training scenario: Cloud Heights Identity Center (simulated). No real organisation, people or systems.

- Prepared by: Catasia Williams
- Audience: Cloud Heights leadership
- Length: 306 words (target about 250–400)
- Full technical detail: [technical-incident-report.md](technical-incident-report.md)

## What happened?
An account belonging to an employee named Drew was disabled following the employee's termination. The available evidence indicates that the appropriate administrative actions were taken to deactivate the account as part of the organization's employee offboarding process. This action was intended to remove Drew's access to organizational systems and applications after their employment ended. Disabling the account helps prevent former employees from retaining access to company resources after termination. The account deactivation was documented as part of the organization's efforts to manage employee access and maintain appropriate security controls. The evidence confirms that steps were taken to disable the account; however, it does not provide additional details about the specific actions performed or independently establish whether the account was successfully deactivated. The event relates specifically to the removal of an employee's account access following termination.

## Why does it matter?
Disabling accounts when an employee leaves the organization is an important security measure because it helps prevent former employees from retaining access to company systems, applications, and potentially sensitive information. However, although the evidence shows that the necessary actions were performed, it does not confirm that the account was successfully disabled or that the intended security measures are working as expected.

## What did we find?
There is currently insufficient evidence to verify that Drew can no longer authenticate or gain access to the account. Completing the administrative steps alone does not guarantee that access has been fully revoked.

## What should happen next?
It is recommended that an authorized IT administrator perform an access verification test by attempting to sign in to the disabled account or otherwise checking its authentication status through the appropriate administrative tools. The test should confirm that the account is disabled and that authentication attempts are rejected. The results should also be documented to provide evidence that the offboarding process was completed successfully. If the account remains accessible, the issue should be investigated and corrected immediately.
