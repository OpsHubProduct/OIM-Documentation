{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

## New Connector(s)
* **Windchill PLM** *
  * **Supported Version:** * 13.x
  * **Supported Entity:** Issue [Soft type/Subtype of Problem Reports]

## Enhancements

### common
* <code class="expression">space.vars.SITENAME</code> now meets WCAG 2.2 Level AA standards to support better accessibility for all users.

### Codebeamer
* Improved support for synchronizing inline attachments and images in Codebeamer for items created through duplication. 
  * In Codebeamer, duplicated items do not contain the actual attachments or inline images; instead, these are referenced from the original entity.    * As in Codebeamer, when item is duplicated, it doesnot contain the actual attachment/inline, it was referenced from the older entity. 
  * For more information about this known behavior, refer to item #26 in the connector guide under [known behaviour or limitation](../connectors/codebeamer.md#known-limitationsbehavior) section. 

## Major Bugs

### Common
* Resolved an issue where attachments were sometimes removed and re-added because updates were incorrectly detected, preventing unnecessary updates in the target system.

### Azure DevOps Server/Services
* Resolved an issue where processing failure was observed with message "OH-Connector-0071: Error occurred while updating entity X because of java.lang.NullPointerException: Cannot invoke "com.opshub.eai.core.interfaces.IHistorySupport.saveOldAttachments" 

### Jira
* Resolved an issue where a job error occurred with the message "com.opshub.exceptions.eai.OIMRunTimeException: java.net.URISyntaxException: Illegal character in path at index 48" where Jira Cloud as the source system.
  * **Use case:** The issue was caused by an invalid link property in a weblink within a changelog. This occurred when data had been previously migrated from a Jira Data Center environment to Jira Cloud using the Jira Cloud Migration Assistant (JCMA).
* Resolved an issue where frequent temporary job errors occurred with the message "com.opshub.exceptions.eai.OIMRunTimeException: java.lang.NullPointerException: Cannot invoke 'java.lang.Integer.intValue()' because the return value of 'java.util.Map.get(Object)' is null".
* Resolved an issue where a job error occurred with message "Invalid value type returned by system connector (<System Name>) for field <Multi select field>, expected type String[] or List Failed to execute method"
  * **Use case:** When Jira Service Management projects are mapped in the integration, a job error may occur if the data type of a multi-select field differs between the actual and expected values for a non-mapped field. 

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs

* Resolved an issue where processing failure was observed with message "OH-Connector-0071: Error occurred while updating entity X because of java.lang.NullPointerException: Cannot invoke "com.opshub.eai.core.interfaces.IHistorySupport.saveOldAttachments"
* Resolved an issue where processing failures occurred when a work item revision contained a deleted area path or iteration.

{% endif %}  
