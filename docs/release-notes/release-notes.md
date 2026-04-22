{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

***

# New Version(s)
* Apache Tomcat: 10.1.54
* Azure DevOps Server: 2025

# New Entities
* **Aha**: Goal, Idea
* **SolarWinds Service Desk**: Catalog Items, Change Catalog, Problems, Releases, Solutions

# Enhancements

## Common
* Added support for folder search functionality.
* Improved the forgot/reset password feature to work without requiring SMTP configuration in OpsHub. 
* Enhanced the Welcome page to hide default credentials after upgrade for security reasons.

# Major Bugs

## Common
* Resolved an issue where formatting did not correctly convert from Markdown to Wiki format.
* Resolved an issue where upgrades failed due to MySQL connection problems when <code class="expression">space.vars.SITENAME</code> was deployed with a MySQL database. 
* Resolved an intermittent global failure that occurred due to a null return from com.opshub.eai.OIMEventGenerator.getSystem(), resulting in the message: "Cannot invoke 'com.opshub.dao.core.Systems.getSystemType()' because the return value is null.
* Resolved an issue where the source item kept updating in a cyclic manner when the sync confirmation field was configured. 
* Resolved an intermittent global failure caused by a sudden database connection issue due to a network drop.
* Resolved an issue where the activate/inactivate all integrations feature did not work as expected when more than 10 integrations were configured within a single integration group.
* Resolved an issue where rule-based routing did not work as expected when filter criteria were applied to a multivalued field.
* Resolved an issue where a user-friendly error message was not displayed when attempting to log in to the UI while the database connection for <code class="expression">space.vars.SITENAME</code> was broken.
* Resolved an issue where an error popup appeared while opening the audit for a processing failure.

## Azure DevOps Server/Services
* Resolved an issue where the Test Run integration triggered repeated API calls during recovery, causing unexpected behavior and high CPU usage.
* Fixed a global failure that occurred with the message com.opshub.exceptions.eai.OIMRunTimeException: java.lang.NullPointerException: Cannot invoke "com.opshub.eai.tfs.client.handlers.ReleasePipelineEntityHandler$AgentPoolIdWithQueueName.getQueueName()" because "agentPoolIdWithQueueName" is null, which happened when an agent associated with the pipeline was deleted in the source.

## Codebeamer
* Resolved an issue where processing failure was observed due to a field marked mandatory for a specific status was incorrectly treated as mandatory for all statuses in <code class="expression">space.vars.SITENAME</code>. 

## GitHub
* Resolved an issue where disk space usage increased during GitHub integration due to temporary storage.  

## Jama Connect
* Resolved an issue where tag parsing failed due to API changes in Jama, which now return tags bundled within double quotes.
  * Previously, Jama logged tag changes individually in history, but it now records them in a quoted batch format.

## Jira
* Fixed a processing failure in Zephyr Scale where the message OH-OIM-0019: Unsupported operation 'Attachment' for OIM connector occurred when a Test Case had a Test Step field type that did not support attachments. 

## Monday.com
* Resolved a global error that occurred when items in Monday.com were created or updated via automation.
  * In Monday.com, when an item is created or updated via automation, the automation user does not have a creator ID or name, which causes the issue.  

## ServiceNow/ServiceNow Express
* Resolved an issue where API requests were rejected because complex criteria queries exceeded the query length limit in a GET call.
  * This issue occurs only when the integration is configured with a complex and lengthy criteria filter, with ServiceNow used as the source system. 

## Tricentis qTest
* Resolved an issue where a processing error occurred with the message {"status":403,"title":"Forbidden","message":"Access is denied"} when calling the user search API, even though the service account had the required permissions.

## Zephyr Enterprise
* Resolved an issue where the folder hierarchy was not correctly preserved during synchronization.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs  
* Resolved an issue where the Test Run migration triggered repeated API calls during recovery, causing unexpected behavior and high CPU usage.
* Resolved a global failure that occurred with the message com.opshub.exceptions.eai.OIMRunTimeException: java.lang.NullPointerException: Cannot invoke "com.opshub.eai.tfs.client.handlers.ReleasePipelineEntityHandler$AgentPoolIdWithQueueName.getQueueName()" because "agentPoolIdWithQueueName" is null, which happened when an agent associated with the pipeline was deleted in the source.

{% endif %}  
