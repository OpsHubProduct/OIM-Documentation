## Description

Migrating <code class="expression">visitor.claims.unsigned.product</code> to new version will ensure that the application includes new features and improved functionality.

## Solution  
{% if "OM4ADO" === visitor.claims.unsigned.product %}  
Make sure that the [Migration Pre-requisites](../../../manage/upgrade/upgrade-application-om4ado.md#pre-upgrade-checklist) steps are followed before migrating to new version.
Once the pre-requisites are met, follow one of the below section
{% endif %}
{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}  
Make sure that the [Pre-Upgrade Checklist](../../../manage/upgrade/upgrade-application.md#pre-upgrade-checklist) steps are followed before migrating to new version.
Once the pre-requisites are met, follow one of the below sections.
{% endif %}

- [Steps to migrate on Windows](../../../manage/upgrade/upgrade-application.md#migration-steps-for-windows)  
  {% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}  
- [Steps to migrate on Linux](../../../manage/upgrade/upgrade-application.md#migration-steps-for-linux) 
{% endif %}

Once migration is completed successfully, follow these [Post Migration Steps](../../../manage/upgrade/upgrade-application.md#post-migration-steps-for-windows-and-linux).

In case the migration fails, you can check for the cause of failure in `Migration.log` file located under `logs` folder at <code class="expression">space.vars.OIM</code> `<installation_path>`.