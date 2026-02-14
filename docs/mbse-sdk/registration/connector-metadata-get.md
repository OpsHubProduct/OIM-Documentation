# API Name

API Name: Connector Metadata – Get

---

# Overview

This API returns connector metadata information used by MBSE Core to register the connector.

The metadata returned by this API defines:

- Supported connector features
- Configuration fields shown in 'System Configuration' screen of OIM.
- Validation rules
- Dynamic lookup behavior
- Screen-level visibility (System configuration / Integration source configuration / Integration target configuration).

Connector responsibility:

- Prepare all configuration fields required for connector registration.
- Define supported features.
- Provide UI configuration metadata.

---

## API URI

```bash
GET: /mbse/api/1.0/connector-metadata
```

---

## Response Payload

```json
{
  "enableFeatures": [
    "CURRENT_STATE_SYNC_FLAG",
    "REMOTE_ID_LINK",
    "TARGET_LOOKUP",
    "CRITERIA",
    "MAPPED_DATA_RETRIEVAL"
  ],
  "additionalMetadata": {
    "userSearchOnUserNameSupported": true,
    "userSearchOnEmailSupported": true,
    "multiEntityTypePollingSupported": true,
    "multiEntityWritingSupported": false
  },
  "fields": [
    {
      "internalName": "authType",
      "displayName": "Authentication Type",
      "tooltip": "Select authentication type",
      "required": true,
      "fieldType": "DROP_DOWN",
      "lookup": {
        "staticValues": [
          {
            "internalName": 1,
            "displayName": "Basic Authentication"
          }
        ],
        "dynamicLookupKey": null
      },
      "defaultValue": null,
      "validation": null,
      "fieldOrder": 1,
      "parent": null,
      "screens": [
        "SYSTEM_CONFIG",
        "INTEGRATION_SOURCE_CONFIG",
        "INTEGRATION_TARGET_CONFIG"
      ]
    }
  ]
}
```

---

# Response Parameters

## Root Level

| Name | Required | Type | Description |
|------|----------|------|-------------|
| enableFeatures | Yes | List\<ENUM\> | List of features supported by the connector. |
| additionalMetadata | No | Object | Additional capabilities supported by the connector. |
| fields | Yes | List\<MetadataField\> | List of configuration fields displayed in MBSE UI. |

---

## enableFeatures

Supported feature values:

- `CURRENT_STATE_SYNC_FLAG`
- `REMOTE_ID_LINK`
- `TARGET_LOOKUP`
- `CRITERIA`
- `MAPPED_DATA_RETRIEVAL`

### Feature Description

| Feature | Description |
|----------|------------|
| CURRENT_STATE_SYNC_FLAG | Enables syncing only the latest element state when using entity-wise history polling. |
| REMOTE_ID_LINK | Stores remote element ID and link mapping across systems. |
| TARGET_LOOKUP | Enables searching target system before writing data. |
| CRITERIA | Enables filtering elements based on configured criteria. |
| MAPPED_DATA_RETRIEVAL | Enables fetching only mapped fields if supported by the end system. |

---

## additionalMetadata

| Name | Required | Type | Description |
|------|----------|------|-------------|
| userSearchOnUserNameSupported | No | Boolean | Whether user search by username is supported. |
| userSearchOnEmailSupported | No | Boolean | Whether user search by email is supported. |
| multiEntityTypePollingSupported | No | Boolean | Whether multiple element types can be polled in a single request. |
| multiEntityWritingSupported | No | Boolean | Whether multiple element types can be written in a single request. |

---

## fields

Each field represents a configuration input shown in system configuration screen of OIM`.

| Name | Required | Type | Description |
|------|----------|------|-------------|
| internalName | Yes | String | Unique internal identifier. |
| displayName | Yes | String | Label shown in UI. |
| tooltip | No | String | Help text for the field. |
| required | Yes | Boolean | Whether field is mandatory. |
| fieldType | Yes | ENUM | Type of UI input control. |
| lookup | Conditional | Object | Lookup configuration for dropdown types. |
| defaultValue | No | String | Default value of field. |
| validation | No | Object | Validation configuration. |
| fieldOrder | Yes | Integer | Display order in UI. |
| parent | No | Object | Parent field dependency configuration. |
| screens | Yes | List\<ENUM\> | Screens where field should appear. |

---

## Supported Field Types

- `TEXT_BOX`
- `TEXT_AREA`
- `DROP_DOWN`
- `PASSWORD`
- `RADIO_BUTTON`
- `CHECKBOX`
- `URL`
- `EMAIL`
- `JSON`
- `XML`
- `NUMERIC`
- `MULTI_SELECT_DROP_DOWN_WITH_CHECKBOX`

---

## Lookup Configuration

### Static Lookup

```json
"lookup": {
  "staticValues": [
    {
      "internalName": 1,
      "displayName": "Basic"
    }
  ],
  "dynamicLookupKey": null
}
```

### Dynamic Lookup Keys

- `ALL_SYSTEM`
- `ALM_SYSTEM`
- `TIME_ZONE`
- `ENTITY_FIELDS`
- `CONFIG_FIELDS`
- `DATABASE_TYPE`

---

## Validation Configuration

| Name | Description |
|------|-------------|
| name | Name of validation rule |
| regex | Regex pattern |
| failureMessage | Error message shown on failure |

Example:

```json
{
  "name": "Version Validation",
  "regex": "[1-9]{1,2}\\.[0-9]{1,2}\\.[0-9]{1,2}",
  "failureMessage": "Please provide valid version in form x.y.z"
}
```

---

## Parent Field Configuration

Used to control field visibility.

| Name | Description |
|------|-------------|
| internalName | Parent field internal name |
| fieldValues | Field is visible only if parent value matches |
| fieldRegex | Regex-based visibility control |

---

## Screens

Defines where the field is visible:

- `SYSTEM_CONFIG`
- `INTEGRATION_SOURCE_CONFIG`
- `INTEGRATION_TARGET_CONFIG`

---

# Behavior Rules

1. All fields must have unique `internalName`.
2. `fieldOrder` must define UI order.
3. `lookup` must be provided for dropdown types.
4. Validation rules must be syntactically correct.
5. Parent-child dependencies must not create circular references.
6. The connector must return complete metadata in a single response.

---

# Example (Multiple Fields)

```json
{
  "enableFeatures": [
    "CURRENT_STATE_SYNC_FLAG",
    "REMOTE_ID_LINK"
  ],
  "additionalMetadata": {
    "userSearchOnUserNameSupported": true,
    "userSearchOnEmailSupported": true,
    "multiEntityTypePollingSupported": true,
    "multiEntityWritingSupported": false
  },
  "fields": [
    {
      "internalName": "serverUrl",
      "displayName": "Server URL",
      "tooltip": "Provide base server URL",
      "required": true,
      "fieldType": "URL",
      "lookup": null,
      "defaultValue": null,
      "validation": null,
      "fieldOrder": 1,
      "parent": null,
      "screens": ["SYSTEM_CONFIG"]
    }
  ]
}
```

---

# Design Rationale

This API defines:

- Connector capability model
- UI configuration schema
- Feature flags
- Dynamic behavior support

Without this API, the connector cannot be registered or configured.

This API must be stable, deterministic, and backward-compatible.
