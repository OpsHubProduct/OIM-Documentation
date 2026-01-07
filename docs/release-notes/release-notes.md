{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# New Connector(s)  
* [**SolarWinds Service Desk**](../connectors/solarwinds-service-desk.md)  
  * Version: SaaS
  * Supported Entities: Incidents, Changes

# New Entities
* **Azure DevOps Server/Services** : Variable Groups

# New Enhancements  

## Common  
* Added support for the Trends and Metrics Dashboard.
  * The Trends dashboard provides a quick view of synchronization activity, project configuration patterns, and failure insights across **<code class="expression">space.vars.SITENAME</code>**. 
  * Users can monitor sync volume, identify high- or low-activity areas, track project growth across systems, and drill down into specific systems, integrations, projects, and entity types for deeper analysis.
  * For more details, refer to the [trends and metrics](../integrate/trends-and-metrics.md) documentation.
* Added support for OAuth 2.0 authentication in the SMTP system. 
  * For setup instructions, refer to the [SMTP configuration](../help-center/troubleshooting/configure-post-failure-notification.md#smtp-configuration) section in the failure configuration guide.

# Major Bugs

## Common
* Resolved an issue where updating User Overwrite settings in the Integration configuration via REST APIs did not work as expected. 
* Resolved an issue where updates from the source HTML field were skipped for the target plain text field when conflict handling was enabled and the conflict strategy was set to "Target wins".
* Resolved an issue where a java.lang.NumberFormatException occurred when the source HTML field contained RGB values in percentage format.

## Azure DevOps Server
* Resolved an issue where a job error occurred during widget synchronization.
  * Use case: When a release pipeline was linked to widgets, an invalid URL was generated while fetching release pipeline details, resulting in a "connection timed out" error.

## GitHub
* Resolved a job error where a 502 Bad Gateway was encountered while retrieving commits due to a large volume of data from GitHub.
  * To change the amount of data fetched, update the "Fetch size for polling commits" field in the GitHub system configuration form.
* Resolved an issue where commits were skipped due to rate limiting when the rate-limit headers were returned with HTTP 200 instead of 429 or 403.

## IBM ClearQuest
* Resolved an issue where a job error occurred while retrieving user information from ClearQuest using a simple system query. 
  * **Action:** Configure dedicated queries in IBM ClearQuest to prevent this issue. Refer to the [post-migration checklist](../manage/upgrade/post-migration-checklist.md#addition-of-new-personal-queries-for-ibm-clearquest-system) for details.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# New Entities
* **Azure DevOps Server/Services** : Variable Groups

# Major Bugs
* Resolved an issue where a job error occurred during widget migration.
  * Use case: When a release pipeline was linked to widgets, an invalid URL was generated while fetching release pipeline details, resulting in a “connection timed out” error.

{% endif %}  
