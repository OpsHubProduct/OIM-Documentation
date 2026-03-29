{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

***  

# New Version(s)
* Broadcom Service Desk Manager: 17.4.3

# Enhancements

## Common
* Added support for retrieving usage reports of <code class="expression">space.vars.SITENAME</code>.
  * For details on exporting usage reports, refer to the [documentation guide](../manage/advanced-utilities/usage-reports.md).
* Introduced a password complexity policy for users created to log in to <code class="expression">space.vars.SITENAME</code>.

## Jira Cloud
* Added support for API Token and OAuth authentication for the Jira Service User.
  * For prerequisites and setup instructions, refer to the connector guide of [Jira](../connectors/jira.md). 

## Tricentis Tosca
* Added support for removing link in Tricentis Tosca.

# Major Bugs

## Monday.com
* Resolved an issue where processing failed when a custom status field contained an empty label value.

## Tricentis qTest
* Resolved an issue where a processing error occurred during module creation (with checkAndCreate enabled), returning the message "status":400,"title":"Bad Request","message":"name size must be between 1 and 500"

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs  
* Resolved an issue where a job error occurred while retrieving Test Run data when more than 200 test cases were attached to a run.
* Resolved an issue where a job error occurred while retrieving test results generated from automated runs, where associating a test case, test plan, or test suite is not required.

{% endif %}  
