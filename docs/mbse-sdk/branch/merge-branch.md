# API Name

API Name: Branch – Merge

---

# Overview

This API merges the specified branch into the main (default/master) branch of the given project.

MBSE Core uses this API to:

- Merge temporary or synchronization branches
- Consolidate changes into the primary branch
- Finalize branch-based operations

Connector responsibility:

- Merge the branch identified by `branchId` into the main/master branch.
- Ensure the merge operation is scoped to the given `projectId`.
- Handle merge conflicts according to end system capabilities.
- Return appropriate HTTP status codes based on merge outcome.

---

## API URI

```bash
POST: /mbse/api/1.0/branches/{branchId}/merge
    ?projectId={projectId}
```

---

## Path Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| branchId  | True      | String | ID of the branch to be merged into the main/master branch. |

---

## URI Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| projectId | True      | String | ID of the project in which the branch exists. |

---

## Behavior Rules

1. The merge must occur within the context of the provided `projectId`.
2. The specified branch must be merged into the main/master branch.
3. Connector must:
    - Call the end system’s merge API.
    - Ensure merge consistency.
4. If merge is successful:
    - Return HTTP `204 No Content`.
5. If branch does not exist:
    - Return HTTP `404 Not Found`.
6. If merge conflicts occur and are not auto-resolved:
    - Return HTTP `409 Conflict`.
7. Connector must not silently ignore merge failures.

---

## Response

This API does not return a response body.

### Successful Merge

HTTP Status: `204 No Content`

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid request parameters. |
| 404        | Branch not found in the specified project. |
| 409        | Merge conflict or merge not allowed. |
| 500        | Internal server error during merge operation. |

---

## Example Use Case

### Merge Branch into Main

```bash
POST /mbse/api/1.0/branches/branch_20260214123045/merge?
projectId=123
```

---

## Implementation Guidelines

- Ensure the branch belongs to the specified project before attempting merge.
- Validate that the branch is not already the main/master branch.
- If the end system generates a new revision during merge:
    - Ensure revision history remains consistent.
- If merge conflicts occur:
    - Either auto-resolve (if supported) or return `409 Conflict`.
- Do not return partial success responses.

---

## Design Rationale

This API completes the branch lifecycle by enabling:

- Controlled integration of branch changes
- Revision history consolidation
- Deterministic synchronization workflows

By clearly separating:

- Branch creation
- Branch deletion
- Branch merge

The MBSE layer remains structured, predictable, and integration-safe.
