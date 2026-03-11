{% if "OpsHub Integration Manager" === space.vars.SITENAME %}

***  

# Major Bugs

## Common
* Resolved an issue where a job error occurred with the message: "OH-Connector-0070: Error occurred while creating entity because of java.lang.ClassCastException: class java.util.LinkedHashMap cannot be cast to class java.lang.String".
  * Use case: This issue occurred when a target field was defined as type Text, but due to advanced mapping, a Map value (LinkedHashMap) was passed instead of a String. During the recovery process, the system attempted to compare the value assuming it was a String, which resulted in the ClassCastException.
* Resolved an issue where end system criteria storage did not work as expected when the criteria storage field was empty.
* Resolved an issue where the log settings could not be opened and an error occurred if the integration had never been activated.
* Resolved an issue where a processing failure occurred with the error message: "OH-Connector-0071: Error occurred while updating entity X because of java.lang.NullPointerException: Cannot invoke com.opshub.eai.EAIAttachment.getAttachmentReferenceTypes() because targetAttachment is null. Failed to execute method OIMAdapter::processInlineMentionedAndInlineFielsOnComment with (8) parameters."
  * This issue happened when a source attachment, referenced in a rich text field, was deleted. The system attempted to process the deleted attachment for auto-upload, resulting in a NullPointerException.

## Azure DevOps Server/Service
* Resolved an issue where incorrect test execution duration data was synchronized during Test Result integration when source and target both are Azure DevOps Server/Services.
* Resolved an issue where a processing failure occurred when the source system was Azure DevOps Service, the organization URL used for connection contained dev.azure.com, and the Multi-Iteration field was mapped for the Test Result entity.

## Codebeamer
* Improved the error message shown when a user attempts to synchronize Test Step Results for a Parent Test Run.
  * In Codebeamer, synchronizing a Test Run automatically creates a Child Run under a Parent Run, and several fields of the Parent Run are calculated based on the Child Run.
  * Because of this relationship, synchronizing Test Step Results directly for the Parent Run is not supported.

## GitHub
* Resolved an issue where a global failure occurred with the error message "java.lang.UnsupportedOperationException: User Lookup from email is not supported for GitHub" in scenarios where a GitHub user's name matched their email address.
* Resolved an issue where a NullPointerException was observed while synchronizing Milestones for the Issue entity type. 

## Jira Cloud
* Resolved an issue where, when Include Comment Author Details was enabled and the Jira source field was mapped to the OH Comment field in the target system, the comment body displayed the author as the user's internal ID instead of their name or email.
  * This typically occurred when the author's profile visibility was restricted in Jira Cloud.
* Resolved an issue where warnings returned by Xray were ignored when the API response status code was 200.

## ServiceNow/ServiceNow Quick Connect
* Resolved an issue where revisions were jumbled and multiple events were created for the same revision after upgrading <code class="expression">space.vars.SITENAME</code> to version 7.217.

{% endif %}

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}

# Major Bugs
* Resolved an issue where incorrect test execution duration data was migrated during Test Result migration.
* Resolved an issue where a processing failure occurred when the source system was Azure DevOps Service, the organization URL used for connection contained dev.azure.com.

{% endif %}  
