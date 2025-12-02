{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# New Connector(s)
* **[Monday.com](../connectors/monday.md)**
  * **Supported Version:** SaaS
  * **Supported Entities:** Board items, Board sub items

# New Version(s)
- Java Development Kit(JDK): 17.0.17

# New Enhancements

## ServiceNow Express
* Added support for custom transition APIs.
  * Refer to the connector documentation on [how to enable custom transition APIs](../connectors/servicenow-quick-connect.md#5-configure-transition-apis) through the metadata JSON.

# Major Bugs

## Common
* Resolved an issue where generating the global ID took excessive time when multiple integrations were performing create and update operations concurrently on a large number of entities. 

## Azure DevOps Server/Services
* Resolved an issue where processing error observed with message "OH-TFS/AzureDevOps-0094: Error occurred while loading entity object using REST API for the URL `https://dev.azure.com/<org_name>/_apis/wit/workitems/-1?$expand=all&api-version=1.0` due to error 404 Not Found."
  * Use case: This issue occurred when creating a work item in Azure DevOps Server/Services as the target system, where the comment included referenced attachments/documents at the creation time.

## Gerrit
* Resolved an issue where synchronization failed to work as expected due to double encoding of the changeid field for the change entity. 

## GitHub
* Resolved an issue where a global error occurred with the message: "com.fasterxml.jackson.databind.exc.MismatchedInputException: Cannot deserialize value of type java.lang.String from Object value (token JsonToken.START_OBJECT)".
  * Use case: This occurred during pull request integration from GitHub when the auto_merge field contained data that caused a parsing error due to a type mismatch.

## Jama
* * Resolved an issue where the data for non-history field such as 'description' was cleared and then restored, causinf extra updates in the end system. 

## ServiceNow Express
* Resolved an issue that caused a processing error with the message: “java.lang.NullPointerException: Cannot invoke 'java.util.Map.get(Object)' because 'entityDetails' is null.”
  * Use case: This occurred when ServiceNow was customized such that, after item creation, the default sys_id key in the response was replaced with a different identifier. 
  * **Action**: Refer to the connector documentation for guidance on [configuring additional metadata for this specific use case](../connectors/servicenow-quick-connect.md#configure-additional-metadata-for-specific-use-cases). 
* Resolved an issue that caused a processing error with the message: "OH-ServiceNow-1004: Incorrect date format for value 07/11/2025 07:40:00 AM. Expected date value should be in format yyyy-MM-dd HH:mm:ssXXX."
  * **Action**: Refer to the connector documentation for guidance on [configuring additional metadata for date formats](../connectors/servicenow-quick-connect.md#1-configure-date-format).
* Resolved an issue where the end system’s error message was not populated correctly when a 404 error code was received from the ServiceNow.

## Verisium Manager
* Resolved an issue where a processing failure occurred when a delete job was configured with soft-delete enabled while using Verisium Manager as the target system. 

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

{% endif %}  
