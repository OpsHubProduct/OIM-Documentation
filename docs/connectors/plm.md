# Windchill PLM Integration Guide

# Prerequisites

### Creating an Integration User

Before you begin, you need to set up a dedicated user account in Windchill PLM that will be used specifically for this integration. This dedicated user is called an "Integration User".
- This user will handle all data synchronization between Windchill PLM and your other system
- This user shouldn't perform any other action from Windchill PLM's user interface

### Required Scope/Permission

* When configuring an integration with Windchill PLM, it’s essential to assign only the necessary permissions based on the planned operations and business requirements. These permissions control what data the integration user can access or modify, ensuring both functionality and security within Windchill PLM.

* To **add or remove permissions** for an integration user in Windchill PLM, use the Policy Administration tools, which allow administrators to manage access at the domain, role, or object level as described in the [Security Management Permissions Reference](https://support.ptc.com/help/windchill/plus/r12.0.2.0/en/index.html#page/Windchill_Help_Center/SecurityMgmtPermissionsRef.html)

> **Note**: If required permissions are missing or insufficient, the integration may fail or restrict operations. Always ensure that the integration user has the appropriate permissions before beginning the setup.

#### Permissions Required for Integration User in Windchill PLM

The integration user must have the following Windchill PLM permissions:

- **Read**: Ability to view items
- **Create**: Ability to create new items
- **Modify, Modify Identity**: Ability to update and change item fields
- **Modify Content**: Ability to attach files to items
- **Download**: Ability to download attached files
- **Set State**: Ability to change the lifecycle state of items (e.g., moving from "Open" to "In Progress")

These permissions should be granted for all products and entities that you plan to synchronize as part of the integration.

---
# System Configuration
As you kickstart the integration, the user must first configure Windchill PLM system in <code class="expression">space.vars.SITENAME</code>.  Click [System Configuration](../integrate/system-configuration.md) to learn step-by-step process to configure a system. Refer to the following screenshot:

<p><img alt="Windchill PLM System Form Screenshot" src="../assets/PLMSystemForm.png" /></p>

### Form Fields Explained

| **Field Name**               | **What to Enter**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **System**                   | Select **Windchill PLM** from the dropdown list                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **System Name**              | Give this configuration a unique name (e.g., "Production Windchill" or "Windchill Main"). This helps you identify this connection later                                                                                                                                                                                                                                                                                                                                                                         |
| **Instance URL**             | Provide Server URL of the Windchill instance. This URL will be used for communicating with PLM system API. The format of the URL would be: `http://hostname:port/` or `https://hostname:port/`<br><br>**Example**: `https://windchill.yourcompany.com/`                                                                                                                                                                                                                                                         |
| **Username**                 | Provide the username of a dedicated Windchill PLM user who will be used for communicating with the system. This user should have the required privileges to access the end system. For more details on the required privileges, refer to [User privileges](#permissions-Required-for-integration-user-in-windchill-plm) section.                                                                                                                                                                                |
| **Password**                 | Provide the password of the user added in **Username**                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **Metadata Details**         | This is an advanced field for customizing how fields and relationships work. See the [Advanced Configuration](#advanced-configuration-metadata-details) section below for details                                                                                                                                                                                                                                                                                                                               |
| **Base URL for Remote Link** | This is the URL that will be used when creating clickable links back to Windchill PLM.<br><br>**When to use this**: If your Windchill PLM has different URLs for internal use (API) versus external access (user interface), enter the user-facing URL here.<br><br>**Example**: If your API URL is `https://api.windchill.com/` but users access Windchill at `https://windchill.yourcompany.com/`, enter the second URL here.<br><br>If left empty, the system will use the Instance URL for generating links |


### Advanced Configuration: Metadata Details

The **Metadata Details** field allows you to customize how Windchill PLM fields behave during synchronization. This is optional but useful for addressing specific needs. 

#### When Would You Use This?

You might need to use this advanced configuration if:
- Windchill PLM doesn't correctly report whether a field is read-only or editable
- Windchill PLM doesn't correctly report multivalue support for a field
- You need to synchronize custom fields that aren't automatically detected
- You want to specify exact date formats for date fields
- You need to define relationships between different types of items

### Understanding the JSON Structure

The Metadata Details field accepts configuration in JSON format. Here's a template configuration with all possible options explained:

```json
{
  "entities": [
    {
      "internalName": "PTC.ChangeMgmt.Issue",
      "fields": {
        "system": [
          {
            "internalName": "comIssueAssignmentDate",
            "displayName": "Assignment Date",
            "dataType": "date_string",
            "multiselect": false,
            "mandatory": false,
            "readOnly": false, 
            "dateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ"
          }
        ]
      },
      "relationship": {
        "linkTypes": [
          {
            "linkType": "ReferenceObjects",
            "reverseLinkType": "ReferenceObjects"
          }
        ]
      }
    }
  ]
}
```

### JSON Configuration Parameters

#### Entity Level

**`internalName`** (at entity level)
- This identifies the type of item in Windchill PLM you're configuring
- Use the exact internal name that Windchill PLM uses
- **Example**: `"PTC.ChangeMgmt.Issue"` for Issue items

#### Field Level

**`internalName`** (at field level)
- The internal name that Windchill PLM uses for this field
- To modify an existing field, use its exact internal name from Windchill
- To add a new custom field, use the unique name assigned to it in Windchill

**`displayName`**
- The user-friendly name shown in the integration interface
- This is what you'll see when mapping fields

**`dataType`**
- Specifies what type of data the field contains
- Common values: `text`, `lookup`, `date`, `boolean`, `number`
- Use this to correct cases where Windchill doesn't report the correct type

**`multiselect`**
- Set to `true` if the field can hold multiple values
- Set to `false` if it can only hold a single value
- **Example**: A "Categories" field that allows multiple selections would be `true`

**`mandatory`**
- Set to `true` if this field must have a value
- Set to `false` if the field is optional

**`readOnly`**
- Set to `false` to allow the integration to update this field
- Set to `true` to prevent updates to this field
- **Useful when**: Windchill reports a field as read-only, but you know it can be updated through the API (like the Status field)

**`dateFormat`**
- Specifies the format for date fields
- Only needed if Windchill uses a non-standard date format

#### Relationship Level

**`linkTypes`**
- Defines how different items can be linked together
- **`linkType`**: The type of link from the current item to another
- **`reverseLinkType`**: The type of link from the other item back to this one

> **Important**: You only need to include fields in the JSON that you want to customize. Standard fields that work correctly don't need to be listed.
> **Note**: Refer to [Get Internal Field Names for Windchill PLM Entities](#get-internal-field-names-for-windchill-plm-entities) to learn how to retrieve the exact entity and field internal names for your Windchill instance.

### JSON Configuration Examples:
1) Make the `status` field writable (set `readOnly` to `false`):

```json
{
  "entities": [
    {
      "internalName": "PTC.ChangeMgmt.Issue",
      "fields": {
        "system": [
          {
            "internalName": "status",
            "readOnly": false
          }
        ]
      }
    }
  ]
}
```

2) Make a field multi-select (set `multiselect` to `true`):
```json
{
  "entities": [
    {
      "internalName": "PTC.ChangeMgmt.Issue",
      "fields": {
        "system": [
          {
            "internalName": "categories",
            "multiselect": true
          }
        ]
      }
    }
  ]
}
```

3) Add a custom mandatory text field `reporter`:
```json
{
  "entities": [
    {
      "internalName": "PTC.ChangeMgmt.Issue",
      "fields": {
        "system": [
          {
            "internalName": "comIssueReporter",
            "displayName": "Reporter",
            "dataType": "text",
            "mandatory": true
          }
        ]
      }
    }
  ]
}
```
---

# Supported Entities

Currently, this integration supports:

- **Issue** (Soft types / Subtypes of Problem Reports)
---

# Mapping Configuration

Map the fields between Windchill PLM and the other system to be integrated to ensure that the data between both the systems synchronize correctly. Refer to [Mapping Configuration](../integrate/mapping-configuration.md) to learn the step-by-step process to configure mapping between the systems.

<p><img alt="Windchill PLM Mapping Configuration Screenshot" src="../assets/PLMMappingConfiguration.png" width="1200"/></p>

### Attachments Configuration

* Windchill PLM supports item-level file attachments.
* Attachments are treated as file entities and must be mapped accordingly in the Mapping Configuration.
* When a file is attached to an item in Windchill PLM, the integration will sync the file as an attachment in the target system.
---

# Integration Configuration

Set a time to synchronize data between Windchill PLM and the other system to be integrated. Also, define parameters and conditions (if any) for integration. Refer to [Integration Configuration](../integrate/integration-configuration.md) to learn the step-by-step process to configure the integration between two systems.

<p><img alt="Windchill PLM Integration Config Screenshot" src="../assets/PLMIntegrationConfig.png" width="2200"/></p>


### Setting Up Synchronization Filters (Criteria Configuration)

You may want to synchronize only specific items from Windchill PLM, rather than everything. For example, you might only want to sync Issues with a certain priority.

**How to set up filters:**

Windchill PLM uses a query language to filter items. The integration supports Windchill's native query format.

#### Understanding Query Syntax

Queries in Windchill follow this pattern:
```
FieldName operator Value
```

**Example**: To find an Issue with a specific ID:
```
ID eq OR:wt.change2.WTChangeIssue:0000001
```

Where:
- `ID` is the field name
- `eq` means "equals"
- `OR:wt.change2.WTChangeIssue:0000001` is the value to match

#### Sample Queries

| **What You Want to Find**                            | **Query to Use**                                                      | **What it Achieves**                                                   |
|------------------------------------------------------|-----------------------------------------------------------------------|------------------------------------------------------------------------|
| Issues with State open                               | `State/Value eq 'OPEN'`                                               | Returns Issues where the `State` field equals `OPEN`                   |
| Issues created after a date and has certain priority | `IssuePriority/Value eq 'HIGH' and CreatedOn gt 2024-01-01T00:00:00Z` | Returns Issues where priority is `High` and created after `2024-01-01` |

#### Important Notes About Filters

- **Navigable properties only**: You can only filter on fields that Windchill considers "navigable"
- Filters on non-navigable properties will either fail or be ignored
- Check [Windchill PLM's documentation on navigational properties](https://support.ptc.com/help/windchill_rest_services/r2.7/en/#page/windchill_rest_services/WCCG_RESTAPIsConfiguringNavigationalProperties.html) for more details

For more information about query options, see [Windchill PLM's Query Parameters documentation](https://support.ptc.com/help/windchill_rest_services/r2.7/en/#page/windchill_rest_services/examples_WCCG_RESTAPIsSupportedQueryOptions.html#).


### Target Lookup Configuration

Before creating a new item in Windchill PLM, you might want to check if it already exists. This prevents duplicate items from being created.

**How it works:**

You provide a query that the integration will use to search for matching items in Windchill PLM. If a match is found, the existing item is updated instead of creating a new one.

**Using placeholders:**

You can use field values from your source system in the search query by wrapping field names in `@` symbols.

**Example:**
```
comUpstreamItem eq @ID@
```

In this example:
- `comTestUpstreamItem` is the Windchill field to search
- `@ID@` will be replaced with the actual ID value from your source system
- The integration will look for a Windchill item where `comTestUpstreamItem` matches the source ID

---

# Known Behaviors and Limitations

- Each synchronization run captures the latest version of the item at that time, not its full history
- Some fields may appear as read-only in the mapping interface, but you can override this in the Metadata Details JSON if the field can actually be updated via APIs. Example, Status field.
- Windchill does not report whether a field supports multiple values. Use the JSON configuration to specify the correct behavior for the field.
- The integration can only sync attached files that are uploaded to an item using **Attach new local file** option.
- Comments and discussions are not synchronized
- While you can read configured relationships, you cannot create or modify relationships through the integration
- New items created by the integration are placed in the base folder of the product container
- The folder field is read-only; items cannot be moved to different folders via the integration
- Only fields that appear in an item's details tab are available for synchronization
- The Metadata Details JSON cannot introduce entirely new entity types to Windchill, It can only modify or add fields to existing entity types, along with relationships.
- Product names containing a single quote (`'`) are not supported

---

# Appendix

### Get Internal Field Names for Windchill PLM Entities

To determine the exact internal names of Entity and Fields for your Windchill PLM instance:

1. Access the Windchill REST API documentation at your Windchill instance.
2. Use the `GetWindchillMetaInfo()` API call (see Windchill REST API docs).
3. Look for these values in the response:
   * **EntityType** → use as `entities[].internalName`
   * **PropertyName** → use as `fields.system[].internalName`