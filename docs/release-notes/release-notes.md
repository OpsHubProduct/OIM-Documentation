{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

---  

# New Connector(s)
* [**Polarion**](../connectors/polarion.md)
  * Version: 
    * On Premise: ALM 2506
    * SaaS*
  * Supported Entities: User Story, Requirement, Epic, Task, Test Case, Issue, Change Request, Release, all system-defined work items, and custom work items

# New Enhancements    

## Broadcom Rally Software
* Added capability to link Defects with Portfolio Items.

## Broadcom Service Desk Manager
* Introduced support for linking Assets and Configuration Items (CIs).

## Jira Cloud
* Enabled support for linking Assets for Jira Service Management within Jira Cloud.

## ServiceNow
* Eliminated the need for additional update or business rule configurations to refresh an item's modified time in ServiceNow after adding attachments to incidents or synced items.

## Tricentis Tosca
* Added support for alternative authentication methods, including Personal Access Token (PAT) and Client Credentials.

## Windchill PLM
* Introduced support for impersonation, allowing the CreatedBy and Modifier fields to reflect the source system user.

# Major Bugs

## Common
* Resolved an issue where users were unable to reset the password for <code class="expression">space.vars.SITENAME</code>.
* Resolved an issue where duplicate comments were created in integration mode after a reconciliation was completed.
  * Use case: When integration mode is temporarily turned off, comments added in the source system are correctly synced during reconciliation, but re-enabling integration may cause previously reconciled comments to sync again, leading to duplicates.

## Aras Innovator
* Resolved an issue where end-system criteria storage was not functioning correctly.

## Azure DevOps Server/Service
* Resolved an issue where a job error occurred while retrieving details for a requirement-based test suite when the associated requirement or user story had been deleted.
* Resolved an issue where end-system criteria storage was not functioning correctly for Test Suite.

## Jira
* Resolved an issue where custom field data was not retrieved due to a naming collision between the custom field’s display name and a system field’s internal name.
* Resolved an issue where API rate limits were not handled correctly in Jira Xray Cloud when retrieving step-level attachments.

## OpenText ALM Octane
* Resolved an issue where entity mentions were not functioning as expected for the Task entity.

## ServiceNow
* Resolved an issue where ambiguous CI associations occurred while using advanced utility methods when multiple CI items shared the same name.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs
* Resolved an issue where updating the system from the <code class="expression">space.vars.SITENAME</code> UI did not refresh cached data, resulting in stale information being displayed.
* Resolved an issue where a job error occurred while retrieving details for a requirement-based test suite when the associated requirement or user story had been deleted.

{% endif %}  
