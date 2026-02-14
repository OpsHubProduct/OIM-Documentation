# API Name

API Name: Element – Add Relation

---

# Overview

This API creates a relation from a source element to a target element.

MBSE Core uses this API to:

- Establish structural relationships
- Create dependencies
- Create realizations
- Create associations and other modeling links

Connector responsibility:

- For the given `elementId` and context:
    - Create a relation in the end system.
- If the end system treats relations as elements:
    - No special implementation may be required beyond standard element creation.
- If the end system represents relations as separate relation elements:
    - Connector may need multiple API calls.
    - Create relation element.
    - Set relation properties or tagged values if required.
- Convert request into end system-specific relation format.

---

## API URI

```bash
POST: /mbse/api/1.0/elements/{elementId}/relations
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &branchId={branchId}
```

---

## Path Parameters

| Name       | Mandatory | Type   | Description |
|------------|-----------|--------|-------------|
| elementId  | True      | String | ID of the source element in the relation. |

---

## URI Parameters

| Name          | Mandatory | Type   | Description |
|---------------|-----------|--------|-------------|
| projectId     | True      | String | ID of the project. |
| elementTypeId | True      | String | ID of the element type of the source element. |
| branchId      | False     | String | ID of the branch. If omitted, default branch behavior applies. |

---

## Request Body

```json
{
  "relationType": "dependency",
  "targetElementId": "requirement_55",
  "targetElementTypeId": "Requirement"
}
```

---

## Request Body Parameters

| Name                | Mandatory | Type   | Description |
|---------------------|-----------|--------|-------------|
| relationType        | True      | String | Type of relation (association, dependency, generalization, realization, etc.). |
| targetElementId     | True      | String | ID of the target element. |
| targetElementTypeId | True      | String | ID of the target element type. |

---

## Behavior Rules

1. The source element must exist within:
    - `projectId`
    - `elementTypeId`
    - Optional `branchId`
2. The target element must exist within the same project (unless cross-project relations are supported).
3. Only one relation must be created per request.
4. Connector must:
    - Call the appropriate end system API to establish the relation.
5. If the relation already exists:
    - Either ignore gracefully or return `409 Conflict` depending on end system behavior.
6. If source or target element does not exist:
    - Return HTTP `404 Not Found`.

---

## Response

This API does not return a response body.

### Successful Creation

HTTP Status: `201 Created` or `204 No Content`

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid input parameters. |
| 404        | Source or target element not found. |
| 409        | Relation already exists or constraint violation. |
| 500        | Internal server error during relation creation. |

---

## Example Use Case

### Add Dependency Relation

```bash
POST /mbse/api/1.0/elements/block_200/relations?
projectId=123
&elementTypeId=Block
```

Request Body:

```json
{
  "relationType": "dependency",
  "targetElementId": "requirement_55",
  "targetElementTypeId": "Requirement"
}
```

---

## Implementation Guidelines

- Validate source element existence before relation creation.
- Validate target element existence before relation creation.
- Ensure branch consistency.
- If relation requires additional metadata:
    - Create relation.
    - Then update additional properties/tags.
- Avoid duplicate relation creation.
- Keep implementation idempotent if possible.

---

## Design Considerations

Different MBSE systems model relations differently:

### Case 1: Relation is implicit
- System directly supports linking elements.
- Single API call required.

### Case 2: Relation is a separate element
- Create relation element.
- Set relation attributes.
- Associate source and target elements.

Connector must abstract these differences and always return consistent behavior.

---

## Design Rationale

This API ensures:

- Controlled relation establishment
- System-agnostic modeling
- Clear source-target mapping
- Flexible implementation for heterogeneous MBSE tools

By isolating relation creation into a dedicated API, the integration layer remains clean, predictable, and extensible.
