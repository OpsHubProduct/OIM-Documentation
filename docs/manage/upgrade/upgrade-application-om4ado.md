---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: false
---

# Upgrading Application Version

An upgrade from the current version to a higher version becomes necessary to include support updates and feature enhancements available in newer versions.

# Upgrade Prerequisites

* Provide the required permissions to database users as mentioned in the [Database Selection](Installation_Steps.md#database-selection) section of the Installation Steps page.
* Follow the instructions mentioned in the [Pre-Upgrade Checklist](#pre-upgrade-checklist) before starting the upgrade process, based on the currently installed version of {{SITENAME}} and the target upgrade version.

# Pre-Upgrade Checklist
> **Note:** There are currently no pre-upgrade checklists available.

# Upgrade Steps

* Stop all migrations.
* Close <code class="expression">space.vars.OM4ADO</code> before starting the upgrade.
* Take a backup of the database. Refer to the [Database Backup](./taking-application-backup.md#database-backup) section.
* Take a backup of the application folder. Refer to the [Application Backup](taking-application-backup.md#application-backup) section.
* Extract the `OM4ADO-V<version>_Migrator.zip` package and execute the installer file.
* When prompted for the existing installation path, provide the same installation directory where the application is already installed and click **Next**.
* After clicking **Next**, the upgrade process will begin. The process may take approximately 4–5 minutes to complete.

# Post-Upgrade Checklist
> **Note:** There are currently no post-upgrade checklists available.
