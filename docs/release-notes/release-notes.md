{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

---  

# Enhancements

## Azure DevOps Server/Services
* Markdown formatting for rich text fields and comments, including inline images and mentions, is now supported for Pull Request entity.

# Bugs

## Common
* Entities were skipped during reconciliation in multi-project integrations where multiple source projects were synchronized into a single target project.

* Unexpected link removal during backward synchronization in out-of-scope re-scope scenarios.
  * Use case: When an entity and its linked items moved out of scope in System 1, the corresponding entities in System 2 were removed. After the project was brought back into scope in System 1 and the entity was recreated in System 2, backward synchronization treated the missing links as removals and incorrectly removed the valid existing links in System 1.

## Codebeamer
* For Codebeamer as the target system, the link sync between Defect and Test Run failed with the following processing failure error message: `OH-Connector-0055: Error occurred while performing operation on Link of the entity. Because of java.lang.NullPointerException: Cannot invoke "java.util.List.stream()" because "mandatoryLinksLst" is null".`

## IBM Engineering Test Management
* For IBM Engineering Test Management as the source system, synchronization failed with the following processing failure error message:`Caused by: org.xml.sax.SAXParseException: The content of elements must consist of well-formed character data or markup.`. This occurred if the entity contained the complex field [like "Approvals" field].

## GitHub
* For GitHub as the source system, project information was not retrieved during Issue entity synchronization.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

{% endif %} 