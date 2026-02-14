# API Name

API Name: Stereotypes – Get Details

---

# Overview

This API returns stereotype metadata for a given UML metatype and list of stereotypes.

MBSE Core uses this API to:

- Retrieve stereotype definitions
- Retrieve tagged value (tag) definitions
- Validate tag data during element creation and update
- Support dynamic modeling capabilities

Connector responsibility:

- For the given `metaType` and `stereotypes`:
    1. Load stereotype definitions from the end system.
    2. Resolve stereotype IDs if required.
    3. Fetch tag definitions associated with those stereotypes.
- Convert the response into `MbseStereotype` format.
- Return consistent and complete stereotype metadata.

---

## API URI

```bash
GET: /mbse/api/1.0/stereotypes
    ?projectId={projectId}
    &metaType={metaType}
    &stereotypes={stereotypes}
    &expandTags={expandTags}
```

---

## URI Parameters

| Name        | Mandatory | Type          | Description |
|-------------|-----------|--------------|-------------|
| projectId   | True      | String       | ID of the project. |
| metaType    | True      | String       | UML metatype of the element (e.g., `uml:Class`, `uml:Signal`). |
| stereotypes | True      | List<String> | Qualified names or names defined in element types JSON for stereotypes. |
| expandTags  | False     | Boolean      | If `true`, include tag definitions in the response. If `false`, return stereotype details without tag definitions. |

---

## Behavior Rules

1. The response must be scoped to:
    - `projectId`
    - `metaType`
2. Only the requested stereotypes must be returned.
3. If `expandTags = true`:
    - Include tag definitions (`tagDefinitions`) for each stereotype.
4. If `expandTags = false`:
    - Return stereotype identifiers without tag definitions.
5. Connector must:
    - Resolve stereotype IDs internally.
    - Map end system tag metadata to `MbsePropertyMeta`.
6. If no matching stereotypes are found:
    - Return an empty list.

---

## Response Payload

### Sample Response

```json
[
  {
    "id": "st_001",
    "name": "SystemBlock",
    "tagDefinitions": [
      {
        "id": "criticality",
        "name": "Criticality",
        "dataType": "LOOKUP",
        "isMandatory": false,
        "isMultiSelect": false,
        "isReadOnly": false,
        "timeUnit": null,
        "dateFormat": null,
        "canBeSetAtElementCreateTime": true,
        "updateStepNumber": 1
      }
    ]
  }
]
```

---

## Response Parameters

### Stereotype Object

| Name           | Required | Type                        | Description |
|----------------|----------|-----------------------------|-------------|
| id             | True     | String                      | Unique identifier of the stereotype. |
| name           | True     | String                      | Name of the stereotype. |
| tagDefinitions | False    | Set<MbsePropertyMeta>       | Tag metadata definitions (if expanded). |

---

### Tag Definition Object (`MbsePropertyMeta`)

| Name                         | Required | Type        | Description |
|------------------------------|----------|------------|-------------|
| id                           | True     | String     | Unique identifier of the tag. |
| name                         | True     | String     | Display name of the tag. |
| dataType                     | True     | Enum       | Data type of the tag. |
| isMandatory                  | True     | Boolean    | Indicates whether the tag is mandatory. |
| isMultiSelect                | True     | Boolean    | Indicates whether the tag supports multiple values. |
| isReadOnly                   | True     | Boolean    | Indicates whether the tag is read-only. |
| timeUnit                     | False    | Enum       | Applicable only if `dataType = TIME_UNIT`. |
| dateFormat                   | False    | String     | Date format if tag represents a date string. |
| canBeSetAtElementCreateTime  | False    | Boolean    | Indicates whether the tag can be set at creation time. |
| updateStepNumber             | False    | Integer    | Update step number if multi-step updates are supported. |

---

## Supported Data Types

The `dataType` field may contain:

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

If `TIME_UNIT` is used, the `timeUnit` value must be one of the following:

- `SECONDS`
- `MINUTES`
- `HOURS`
- `DAYS`

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid request parameters. |
| 404        | Project or metatype not found. |
| 500        | Internal server error while fetching stereotype metadata. |

---

## Example Use Case

### Get Stereotype Metadata with Tag Definitions

```bash
GET /mbse/api/1.0/stereotypes?
projectId=123
&metaType=uml:Class
&stereotypes=SysML::Blocks::Block
&expandTags=true
```

---

## Implementation Guidelines

- Resolve stereotype IDs using end system API.
- Map end system tag definitions accurately.
- Ensure no duplicate tag definitions are returned.
- Maintain consistent data type mapping.
- Avoid returning unrelated stereotype definitions.
- Keep response deterministic.

---

## Design Rationale

Stereotypes define semantic extensions in UML/SysML models.

This API ensures:

- Accurate stereotype discovery
- Proper tag validation
- Safe element creation and updates
- System-agnostic metadata abstraction

By separating stereotype metadata from element metadata, the MBSE SDK maintains clean architectural boundaries and dynamic modeling flexibility.
