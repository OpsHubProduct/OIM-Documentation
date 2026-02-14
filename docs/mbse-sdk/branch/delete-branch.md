# API Name

API Name: Branch – Delete

---

# Overview

This API deletes an existing branch within a given project.

MBSE Core uses this API to:

- Clean up temporary branches
- Remove synchronization branches
- Manage branch lifecycle

Connector responsibility:

- Call the end system API to delete the specified branch.
- Ensure deletion is scoped to the given project.
- Return appropriate HTTP status based on outcome.

---

## API URI

```bash
DELETE: /mbse/api/1.0/branches/{branchId}
    ?projectId={projectId}
```

---

## Path Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| branchId  | True      | String | ID of the branch to be deleted. |

---

## URI Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| projectId | True      | String | ID of the project in which the branch exists. |

---

## Behavior Rules

1. Branch deletion must be scoped to the provided `projectId`.
2. Connector must call the end system API to delete the branch.
3. If deletion is successful:
    - Return HTTP `204 No Content`.
4. If branch does not exist:
    - Return HTTP `404 Not Found`.
5. If branch cannot be deleted due to system constraints (e.g., default branch or protected branch):
    - Return HTTP `409 Conflict` or appropriate error code.
6. Connector must not silently ignore failures.

---

## Response

This API does not return a response body.

### Successful Deletion

HTTP Status: `204 No Content`

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid request parameters. |
| 404        | Branch not found in the specified project. |
| 409        | Branch cannot be deleted (protected/default branch or system constraint). |
| 500        | Internal server error during branch deletion. |

---

## Example Use Case

### Delete Branch

```bash
DELETE /mbse/api/1.0/branches/branch_20260214123045?
projectId=123
```

---

## Implementation Guidelines

- Ensure the branch belongs to the specified project before attempting deletion.
- Do not allow accidental deletion of protected or default branches unless explicitly supported.
- Validate branch existence before deletion if required by end system.
- Return deterministic and meaningful error codes.

---

## Design Rationale

This API provides controlled branch lifecycle management.

By enforcing:

- Project scoping
- Explicit error handling
- No response body on success

The API maintains predictable and safe branch deletion behavior across heterogeneous MBSE systems.
