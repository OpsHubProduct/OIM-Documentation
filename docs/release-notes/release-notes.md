{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

# New Enhancements    

## Azure DevOps Server/Service
* Eliminated the dependency on TFS Services for User, Group, and Team synchronization in Azure DevOps Services.

## Jira
* Added support for step-level results in Zephyr Scale for Jira Cloud.

# Major Bugs

## Common
* Resolved an issue where duplicate links/relationships were created during reconciliation.
* Resolved an issue where projects with slashes in the name (e.g., Test / Test2 / Test3) were incorrectly treated as child projects, even when the target system does not support child project synchronization.
* Resolved an issue where Excel files were not updated when uploaded via the REST (Admin) API.
* Resolved an issue where searching for integrations across folders did not work as expected when the integration name contained special characters treated as wildcards in the database, in environments where <code class="expression">space.vars.SITENAME</code> is installed on MSSQL.
* Resolved an issue where the sample response body was missing from Swagger endpoints for <code class="expression">space.vars.SITENAME</code> REST APIs.

## Azure DevOps Server/Service
* Resolved an issue where a job error occurred while retrieving test runs due to a NullPointerException when the test suite had been deleted, causing OIMEventGenerator::process to fail.
* Resolved an issue where a job error with the message “No content to map due to end-of-input” occurred while retrieving release pipelines when revision IDs were not in a continuous sequence (e.g., revision ID 18 appearing after 16).
* Resolved an issue where integrations skipped certain items even though they met the sync criteria when <code class="expression">space.vars.SITENAME</code> version was above 7.206.

## Broadcom Clarity
* Resolved an issue where mentioned users were not synchronized as expected to Broadcom Clarity as the target system for Project and Task entity fields, due to limitations in end-system support.

## Jira
* Resolved an issue where an intermittent temporary error with the message com.opshub.exceptions.eai.OIMRunTimeException: java.util.ConcurrentModificationException occurred when plugin details were provided in the Jira system form.

## OpenText IT Operations Cloud
* Resolved an issue where a job error occurred when multiple projects were added in a single integration with OpenText IT Operations Cloud (formerly Serena Business Manager) as the source system.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs
* Resolved an issue where a job error occurred while retrieving test runs due to a NullPointerException when the test suite had been deleted, causing OIMEventGenerator::process to fail.
* Resolved an issue where a job error with the message “No content to map due to end-of-input” occurred while retrieving release pipelines when revision IDs were not in a continuous sequence (e.g., revision ID 18 appearing after 16).
* Resolved an issue where migration skipped certain items even though they were eligible for sync when <code class="expression">space.vars.SITENAME</code> version was above 7.206.

{% endif %}  
