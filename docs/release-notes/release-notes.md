{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# Critical Updates & Actions Required
* Due to security requirements, Windows Server versions earlier than 2016 (i.e., Windows Server 2012 and older) are no longer supported operating systems for <code class="expression">space.vars.SITENAME</code>.
  * **Action:** Before attempting to upgrade <code class="expression">space.vars.SITENAME</code>, ensure that the operating system is upgraded to a supported version. Please refer to the [Pre-Migration Checklist](../manage/upgrade/pre-migration-checklist.md). 

# New Versions(s)  
* IBM Rational ClearQuest: 9.x, 10.x
* OpenText ALM Octane: 25.x
* Java Development Kit (JDK): 17.0.18

# New Enhancements  

## Common
* Enhanced the workflow transition XML framework to support updating dependent fields either before or after a transition is executed.
  * For detailed configuration steps, refer to the [Workflow Transition XML](../integrate/configure-integrations.md/mapping-configuration#workflow-transition) documentation.
* Added CAPTCHA validation to the post-registration process to enhance security.

# Major Bugs

## Common
* Resolved an issue where only 1,000 lookup values were being loaded in the UI.
* Resolved an issue where the Entity Type Mapping section overflowed beyond the expected layout block on the View Integration screen.
* Resolved an issue where updating the max retry count on an integration did not reset the failure notification’s notified flag.


## Azure DevOps Server/Service
* Resolved an issue where integrations became stuck after upgrading from versions below 7.204 to 7.215HF2. The issue occurred when, in the mapping configuration for Test Plan or Test Suite, a target field was mapped to a None source field, resulting in a NullPointerException.
* Resolved an issue where job errors occurred after upgrading from versions below 7.216 to 7.217 when Azure DevOps Service was configured with Service Principal authentication. The issue was caused by internal migration attempting to process User, Group, and Team data even when such data did not exist. 
* Resolved an issue where queue details were not retrieved during Release Pipeline integration.
* Resolved an issue where user and entity mentions did not function correctly in rich text fields when the source was Azure DevOps Server versions below 2022.

## Digital.ai Agility
* Resolved an issue where end-system criteria storage was not functioning correctly.

## IBM Engineering Workflow Management
* Resolved an issue where entity mentions were not functioning correctly with the default mention JSON at the system level due to static keywords.

## IBM Rational ClearQuest
* Resolved an issue where case-sensitive SQL Server database collation caused processing failures.
  * To prevent such issues, it is recommended to configure the "OpsHub_emptyQuery" query in the end system as described in the [Query configuration](../connectors/ibm-rational-clearquest.md#queries-configuration) documentation.

## Jira Cloud
* Resolved an issue where the “Tests” link was unavailable between Test Cases and other issue types (e.g., Stories), ensuring accurate Test Coverage reporting in Jira Cloud Xray.

## Monday.com
* Resolved an issue where time details were not retained from Monday.com, as only date information was being captured from the response. 

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs
* Resolved an issue where queue details were not retrieved during Release Pipeline migration.

{% endif %}  
