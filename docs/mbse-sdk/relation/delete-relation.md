# API Name

API Name: Element – Delete Relation

---

# Overview

This API deletes an existing relation between a source element and a target element.

MBSE Core uses this API to:

- Remove structural links
- Remove dependencies
- Remove associations
- Maintain model consistency during synchronization

Connector responsibility:

- For the given source element and relation details:
    - Delete the corresponding relation in the end system.
- If the end system models relations as elements:
    - Delete the relation element.
- If the end system models relations implicitly:
    - Remove the link using the appropriate API.
- Ensure deletion is scoped to the given project and branch.

---

## API URI

```bash
DELETE: /mbse/api/1.0/elements/{elementId}/relations
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &branchId={branchId}
    &relationType={relationType}
    &targetElementId={targetElementId}
    &targetElementTypeId={targetElementTypeId}
```

---

## Path Parameters

| Name       | Mandatory | Type   | Description |
|------------|-----------|--------|-------------|
| elementId  | True      | String | ID of the source element in the relation. |

---

## URI Parameters

| Name                | Mandatory | Type   | Description |
|---------------------|-----------|--------|-------------|
| projectId           | True      | String | ID of the project. |
| elementTypeId       | True      | String | ID of the source element type. |
| branchId            | False     | String | ID of the branch. If omitted, default branch behavior applies. |
| relationType        | True      | String | Type of relation (e.g., Satisfied By, Verifies, Abstraction, dependency, r
