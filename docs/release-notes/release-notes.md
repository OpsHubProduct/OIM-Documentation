{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# New Entities
* **Azure DevOps Server**
  * Release Pipeline**, Service Connection, Task Group : supported in versions 2018 and above
  * Agent Pool : supported in versions 2020 and above
* **Azure DevOps Services**
  * Release Pipeline**, Agent Pool, Service Connection, Task Group

# New Enhancements

## Common
* Improved search capability to help users quickly find Integrations, Mappings, Systems, Workflows, and other components across folders within <code class="expression">space.vars.SITENAME</code>.
  * Additional details are available in the [Search and Navigate](../integrate/search.md) guide.

## GitHub
* Improved GitHub connector behavior by enforcing inclusion of the API version header on every outbound request, rather than relying on GitHub’s default versioning.
  > Note: Note: At this time, only a single API version header is available from GitHub.
  
## Jira Cloud
* Added documentation describing the permission requirements for the scoped base token used with Jira Cloud.
  * For a full list of the minimum permissions the service-account user must have, see the Jira Connector [API Token](../connectors/jira.md#api-token) documentation.

# Major Bugs

## Common
* Resolved an issue where a global error occurred in the delete job synchronization when processing attachments on items that were deleted in the source.
  * Use case: In <code class="expression">space.vars.SITENAME</code> version 7.196 and above, significant improvements were made to attachment and inline synchronization. After upgrading, if a source item was found to be deleted, its attachment and inline information was not processed to align with the new behavior, which could cause the delete job to fail.
* Resolved an issue where reconciliation of some items was skipped when reconciling multiple source projects to a single target project.
  * Use case: If the reconciliation was stopped and then resumed, it interrupted the sequence of items in the queue, causing only items with id greater than the last reconciled one to be processed.
* Resolved an issue where a processing error occurred while transforming events containing empty key tags in the source event XML.

## Broadcom Rally Software
* Resolved an issue where a global error occurred when retrieving link information for a parent item that the service account could not access, resulting in the following NullPointerException: java.lang.NullPointerException: Cannot invoke 'com.opshub.eai.rally.common.RallyDevElement.getAttributes()' because 'portfolioItemObject' is null.
  * Use case: A user story in Rally has a parent feature that the integration cannot access (for example, when the parent resides in a different project). In this scenario, a NullPointerException occurred while parsing link details from the user story response. 

## Database
* Resolved an issue in the Database Connector where attachments were overwritten when multiple attachments with the same name were received from the same source entity.
  * Use case: When adding data from a source system to the database, if a work item contained multiple attachments with the same name, the connector overwrote them and only kept the last occurrence as attachments were stored on the local machine where the <code class="expression">space.vars.SITENAME</code> was deployed.

## IBM Engineering Requirements Management DOORS Next
* Resolved an issue where a global error occurred due to incorrect detection of inline content or documents in rich text fields or comments.

## IBM Engineering Test Management
* Resolved an issue where retrieving external links from IBM Engineering Test Management returned a 400 error and caused synchronization to get stuck.

## ServiceNow Express
* Resolved an issue that caused an error when retrieving data from the `cmdb_ci` table using advanced methods such as `getEntityFieldValue`.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# New Entities
* **Azure DevOps Server**
  * Release Pipeline**, Service Connection, Task Group : supported in versions 2018 and above
  * Agent Pool : supported in versions 2020 and above
* **Azure DevOps Services**
  * Release Pipeline**, Agent Pool, Service Connection, Task Group

# New Enhancements
* License editions have been rebranded: Free is now Community, Premium is now Professional, and Platinum is now Ultimate.
* Support for migrating Area Path and Iteration, previously available only in the Ultimate (formerly Platinum) edition, has now been added to the Professional (formerly Premium) edition.

{% endif %}  
