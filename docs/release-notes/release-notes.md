{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# Major Bugs

## Azure DevOps Server/Services
* Resolved an issue where edited comments were duplicated when the History-based Integration was enabled where Azure DevOps Server/Services as the source system.  
    * Use case: When the integration was configured in history mode, if a work item had already been synced without comments, and comments were later added and edited, some edited comments were duplicated while synchronizing from Azure DevOps Server/Services.

## GitHub
* Resolved an issue where a processing failure occurred with the message **'Invalid Comment Type'** during synchronization of the issue entity to GitHub.

## Jira Cloud/Jira Data Center
* For Jira Cloud, resolved an issue where entities/issues/work items were skipped in cases when the API response did not include newly created or updated issues due to delayed indexing.
* Resolved an issue where an inline image was not synchronized as expected when there was an extra space before the '!' symbol in the image placeholder.  
  * Use case: When reading data from a source system that includes additional image properties such as height or width, a trailing space in those properties could cause an extra space to appear before the closing exclamation mark (for example:  
`!About.png|width=500 !`), preventing proper synchronization.  
    > **Note**: Jira supports the Wiki format in rich text fields. In Wiki format, an inline image is rendered when its name is placed between two exclamation marks (for example: `!Note.jpg!`).

## Microsoft Dynamics 365
* Resolved an issue where entities were skipped when the API response did not include newly created or updated records due to delays in APIs from Microsoft Dynamics 365.

## Tricentis Tosca
* Resolved an issue where a job error occurred with the message `**"Unexpected character ('<' (code 60)): expected a valid value (JSON String, Number, Array, Object, or token 'null', 'true', or 'false')"**` when retrieving test steps from Tosca.


{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs

* Resolved an issue where edited comments were duplicated during migration.  
**Use case:** When migration was configured, if a work item had already been migrated without comments and comments were later added and edited, some edited comments were duplicated during migration from Azure DevOps Server/Services.

{% endif %}  
