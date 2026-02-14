# API Name

API Name: Enumeration Literals – Get

---

# Overview

This API returns enumeration literals (lookup values) for a given property or tag.

MBSE Core uses this API to:

- Populate dropdown values for properties and tags
- Validate lookup values during element creation and update
- Ensure consistent ID-to-name mapping

Connector responsibility:

- Call the end system API to fetch enumeration literals for the specified property or tag.
- Determine whether the identifier refers to a property or a tag using `isTag`.
- Convert the result into `MbseEnumerationLiteral` format.
- Return a list of enumeration literals containing only `id` and `name`.

---

## API URI

```bash
GET: /mbse/api/1.0/properties/{propertyOrTagId}/enumeration-literals
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &isTag={isTag}
```

---

## Path Parameters

| Name              | Mandatory | Type   | Description |
|-------------------|-----------|--------|-------------|
| propertyOrTagId   | True      | String | ID of the property or tag for which enumeration literals are required. |

---

## URI Parameters

| Name           | Mandatory | Type    | Description |
|----------------|-----------|---------|-------------|
| projectId      | True      | String  | ID of the project. |
| elementTypeId  | True      | String  | ID of the element type provided in element types JSON. |
| isTag          | True      | Boolean | Indicates whether `propertyOrTagId` refers to a tag (`true`) or a property (`false`). |

---

## Behavior Rules

1. The API must be scoped to:
    - `projectId`
    - `elementTypeId`
2. If `isTag = true`:
    - Fetch enumeration literals for the specified tag.
3. If `isTag = false`:
    - Fetch enumeration literals for the specified property.
4. The response must contain:
    - Only `id` and `name`.
5. Duplicate literals must not be returned.
6. If no enumeration literals are defined:
    - Return an empty list.

---

## Response Payload

### Sample Response

```json
[
  {
    "id": "1",
    "name": "High"
  },
  {
    "id": "2",
    "name": "Medium"
  },
  {
    "id": "3",
    "name": "Low"
  }
]
```

---

## Response Parameters

### Enumeration Literal Object

| Name | Required | Type   | Description |
|------|----------|--------|-------------|
| id   | True     | String | Unique identifier of the enumeration literal. |
| name | True     | String | Display name of the enumeration literal. |

---

## Ordering Requirement

Enumeration literals should be returned in a deterministic order.

Recommended behavior:

- Sort by `name` in ascending order.
- Alternatively, preserve system-defined ordering if meaningful.

The `MbseEnumerationLiteral` class supports alphabetical sorting by `name`.

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid request parameters. |
| 404        | Property or tag not found. |
| 500        | Internal server error while fetching enumeration literals. |

---

## Example Use Case

### Get Enumeration Literals for a Property

```bash
GET /mbse/api/1.0/properties/status/enumeration-literals?
projectId=123
&elementTypeId=Block
&isTag=false
```

### Get Enumeration Literals for a Tag

```bash
GET /mbse/api/1.0/properties/criticality/enumeration-literals?
projectId=123
&elementTypeId=Block
&isTag=true
```

---

## Implementation Guidelines

- Validate that the property or tag supports lookup values.
- Ensure mapping between end system ID and MBSE ID is stable.
- Do not return UI-only values.
- Ensure no null values are returned.
- Keep response lightweight and efficient.

---

## Design Rationale

Enumeration literals provide controlled vocabulary for:

- Lookup properties
- Tagged values
- Status fields
- Priority fields
- Custom classifications

This API ensures consistent value mapping and safe validation across heterogeneous MBSE systems.
