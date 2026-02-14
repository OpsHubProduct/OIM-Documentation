# API Name

API Name: Properties – Get Metadata

---

# Overview

This API returns metadata information for properties applicable to a given element type.

MBSE Core uses this API to:

- Understand property definitions
- Validate element creation and update requests
- Identify mandatory fields
- Determine data types and formatting
- Support multi-select and lookup behavior
- Support time and date formatting

Connector responsibility:

- Call the end system API to retrieve property metadata for:
    - Given `projectId`
    - Given `elementTypeId`
    - Optional `metaType`
    - Optional `stereotypes`
- Convert the response into `MbsePropertyMeta` format.
- Return complete and accurate metadata definitions.

---

## API URI

```bash
GET: /mbse/api/1.0/properties
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &metaType={metaType}
    &stereotypes={stereotypes}
```

---

## URI Parameters

| Name           | Mandatory | Type          | Description |
|----------------|-----------|--------------|-------------|
| projectId      | True      | String       | ID of the project. |
| elementTypeId  | True      | String       | ID of the element type as defined in element types JSON. |
| metaType       | False     | String       | UML metatype of the element (e.g., `uml:Class`, `uml:Signal`). |
| stereotypes    | False     | List<String> | Qualified names or names provided in element types JSON for stereotypes. |

---

## Behavior Rules

1. Metadata must be scoped to:
    - `projectId`
    - `elementTypeId`
2. If `metaType` is provided:
    - Return properties applicable to that UML metatype.
3. If `stereotypes` are provided:
    - Return stereotype-specific properties.
4. If neither `metaType` nor `stereotypes` are provided:
    - Return base properties applicable to the element type.
5. The response must include:
    - Data type information
    - Mandatory flag
    - Multi-select flag
    - Read-only flag
6. Connector must not return duplicate property definitions.

---

## Response Payload

### Sample Response

```json
[
  {
    "id": "status",
    "name": "Status",
    "dataType": "LOOKUP",
    "isMandatory": true,
    "isMultiSelect": false,
    "isReadOnly": false,
    "timeUnit": null,
    "dateFormat": null,
    "canBeSetAtElementCreateTime": true,
    "updateStepNumber": 1
  },
  {
    "id": "estimatedDuration",
    "name": "Estimated Duration",
    "dataType": "TIME_UNIT",
    "isMandatory": false,
    "isMultiSelect": false,
    "isReadOnly": false,
    "timeUnit": "DAYS",
    "dateFormat": null,
    "canBeSetAtElementCreateTime": true,
    "updateStepNumber": 2
  }
]
```

---

## Response Parameters

### Property Metadata Object

| Name                         | Required | Type        | Description |
|------------------------------|----------|------------|-------------|
| id                           | True     | String     | Unique identifier of the property. |
| name                         | True     | String     | Display name of the property. |
| dataType                     | True     | Enum       | Data type of the property. |
| isMandatory                  | True     | Boolean    | Indicates whether the property is mandatory. |
| isMultiSelect                | True     | Boolean    | Indicates whether the property supports multiple values. |
| isReadOnly                   | True     | Boolean    | Indicates whether the property is read-only. |
| timeUnit                     | False    | Enum       | Applicable only for `TIME_UNIT` data type. |
| dateFormat                   | False    | String     | Date format if property represents a date string. |
| canBeSetAtElementCreateTime  | False    | Boolean    | Indicates whether the property can be set during element creation. |
| updateStepNumber             | False    | Integer    | Update step number if multi-step updates are supported. |

---

## Supported Data Types

The `dataType` field may contain the following values:

- `TEXT`
- `HTML`
- `WIKI`
- `MARKDOWN`
- `LOOKUP`
- `DATE_STRING`
- `BOOLEAN`
- `NUMBER`
- `USERNAME_AS_USER`
- `EMAIL_AS_USER`
- `TIME_UNIT`

### User Data Types

- `USERNAME_AS_USER`
- `EMAIL_AS_USER`

### Time Unit

If `dataType = TIME_UNIT`, the `timeUnit` field value must be one of the following:

Examples:

- `SECONDS`
- `MINUTES`
- `HOURS`
- `DAYS`

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid request parameters. |
| 404        | Project or element type not found. |
| 500        | Internal server error while fetching metadata. |

---

## Example Use Case

### Get Property Metadata for Element Type

```bash
GET /mbse/api/1.0/properties?
projectId=123
&elementTypeId=Block
```

### Get Property Metadata for Specific Metatype and Stereotype

```bash
GET /mbse/api/1.0/properties?
projectId=123
&elementTypeId=Block
&metaType=uml:Class
&stereotypes=SysML::Blocks::Block
```

---

## Implementation Guidelines

- Map end system property definitions accurately to `MbsePropertyMeta`.
- Ensure consistent data type mapping.
- Avoid returning UI-only or system-internal properties unless required.
- Maintain stable property IDs across API calls.
- Validate mandatory flags carefully.
- Return deterministic ordering of properties if possible.

---

## Design Rationale

This API provides the foundation for:

- Validation during create/update
- Lookup value retrieval
- Synchronization correctness

Accurate property metadata ensures the MBSE Connector behaves predictably and integrates cleanly with heterogeneous modeling systems.
