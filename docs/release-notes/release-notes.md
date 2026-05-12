{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

***

# Critical Updates & Actions Required
* Enforced mandatory password reset for all new and default user accounts of <code class="expression">space.vars.SITENAME</code> to ensure compliance with product security requirements and defined password policies.

# Enhancements

## Common
* Improved dashboard view that allows users to click on an integration card and directly navigate to the corresponding integration folder.
* Enhanced rule-based routing to support default routing for entity type movement. For setup guidelines, refer to: [How to configure defaulting for rule-based routing](../integrate/rule-based-routing.md#default-route-configuration-guidelines).
* Enhanced **Transitions & Dependencies** to enforce dependent fields during item updates.
 
## ServiceNow/ServiceNow Quick Connect
* Added support for Catalog Variables.

# Major Bugs

## Common
* Resolved an issue where extra new lines were introduced when syncing content from the source system’s wiki field to the target system’s HTML field.
* Resolved an issue where cyclic sync occurred because changes in inline image height and width were not retained, causing the system to repeatedly detect differences. 

## Azure DevOps Server/Services
* Resolved an issue where enabling OH Soft Delete for test items resulted in hard deletion when the items were deleted in the source system.
  * Clarification: Soft delete is supported only for items that can be restored.
  * In Azure DevOps, only work items support restoration, whereas test items are permanently deleted(hard delete). 
* Resolved an issue where comments were duplicated during creation when both item creation and state transition occurred within the same revision.

## GitHub
* Resolved an issue where the “last processed time” displayed on the integration page showed an incorrect or unexpected date. 

## Jira Cloud
* Resolved an OutOfMemory issue when Jira Cloud was configured as the source in <code class="expression">space.vars.SITENAME</code> with “Child Link” enabled in the mapping configuration.
  * Use case: This happened when the parent item had more than 100 child items, causing repeated retrieval of the same page due to a pagination issue. 

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs  
* Resolved an issue where deletion of the testcase in source, deleted the testcase in target in ongoing migration due to defaulting of delete set to soft-delete which caused an issue as the test items were not supporting restored from bin.

{% endif %}