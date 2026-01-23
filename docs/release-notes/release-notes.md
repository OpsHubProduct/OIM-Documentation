{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# New Enhancements    

## Jira
* Added support to suppress end-system notifications (alerts and email notifications) when updates are made through <code class="expression">space.vars.SITENAME</code>.
  * For guidance on configuration-related changes, refer to [how to suppress end-system notifications](../connectors/jira.md#suppress-end-system-notifications-target-system).
* Added Read/Write support for External Plugin fields. 
  * For information on enabling external plugin fields, refer to the [Jira system configuration](../connectors/jira.md#system-configuration) form.

# Major Bugs

## Common
* Resolved an issue where the integration status was not reflected accurately on the dashboard.
  * Going forward, the integration status behavior is aligned with the Integration View page. 
* Resolved an issue where a ConnectionPoolShutdown error occurred when an exception was raised during a request (for example, an ExecutionException due to an aborted task).
* Resolved a performance issue where slowness was observed while saving (creating or updating) mappings or integrations. 
* Resolved an issue encountered during purging of synced data records with the error message: "com.microsoft.sqlserver.jdbc.SQLServerException: ORDER BY items must appear in the select list if SELECT DISTINCT is specified." 

## Broadcom Rally
* Resolved a job failure caused by the following error: "java.lang.NullPointerException: Cannot invoke 'java.util.Set.add(Object)' because 'this.attachmentReferenceTypes' is null".

## Database
* Resolved a processing error with the message: "OH-Connector-0070: Error occurred while creating entity because of com.microsoft.sqlserver.jdbc.SQLServerException: Violation of PRIMARY KEY constraint."
  * Use case: In environments where multiple integrations write to a single target database and the primary key is configured as an increment (instead of identity), primary key collisions occurred when multiple integration threads attempted to write to the same table.
  * **Action**: Update the primary key policy in the database system configuration from Increment to Identity.
* Resolved a performance issue where slowness was observed while writing data to database tables.

## Jama
* Resolved an issue where some updates were skipped due to delays in the Search API.
  * The probable cause appears to be indexing delays on the end system.

## ServiceNow
* Resolved a processing failure encountered while unlinking associated Configuration Items (CIs) when only a single CI was present on an incident or change request.
  * Use case: When a CI was removed and replaced with a new one at the source system, ServiceNow restricted the removal because at least one CI must always be associated. The fix ensures a new CI is added first (if applicable) before removing the old one to avoid this error.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

{% endif %}  
