## Dos

Follow these best practices while working with <code class="expression">space.vars.OM4ADO</code>.

### Application Server Resources

Ensure that the server hosting <code class="expression">space.vars.OM4ADO</code> is allocated resources according to the **Hardware Prerequisites** section in the **Download and Prerequisites** documentation.

Insufficient server resources may impact migration performance and can lead to failures or instability during migration operations.

For more details, refer to:

[Hardware Prerequisites](../getting-started/prerequisites-om4ado.md#hardware-prerequisites)

---

## Don'ts

Avoid the following practices while working with <code class="expression">space.vars.OM4ADO</code>.

### Do Not Upgrade Without Backup

Do not upgrade <code class="expression">space.vars.OM4ADO</code> without taking a backup of:

- The application directory
- The application database

Taking backups helps restore the environment if issues occur during the upgrade.

### Do Not Skip the Pre-Upgrade Checklist

Before upgrading, always review the **Pre-Upgrade Checklist**.

For more details, refer to:

[Pre-Upgrade Checklist](../manage/upgrade/upgrade-application-om4ado.md#pre-upgrade-checklist)

### Do Not Use HSQL for Production

Avoid using the **HSQL database** in production environments.

HSQL is intended for:

- Evaluation purposes
- Testing environments

It is **not recommended for production use** due to reliability concerns.

For production environments:

- Migrate data from **HSQL** to a supported database server.

For database migration details, refer to:

[Database Migration](../manage/advanced-utilities/database-migration.md)