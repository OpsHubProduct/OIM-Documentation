# API Name

API Name: Branch – Get

---

# Overview

This API retrieves the details of a specific branch within a given project.

MBSE Core uses this API to:

- Validate branch existence
- Retrieve branch metadata
- Support branch-based synchronization

Connector responsibility:

- Retrieve the branch identified by `branchId` within the specified `projectId`
- Return branch details in key-value format
- If the branch does not exist, return HTTP `404 Not Found`

---

## API URI

```bash
GET: /mbse/api/1.0/branches/{branchId}
    ?projectId={projectId}
```

---

## Path Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| branchId  | True      | String | ID of the branch to retrieve. |

---

## URI Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| projectId | True      | String | ID of the project in which the branch exists. |

---

## Behavior Rules

1. The API must retrieve the branch within the context of the given project.
2. If the branch exists:
    - Return branch details.
3. If the branch does not exist:
    - Return HTTP `404 Not Found`.
4. The response must not return unrelated branch data.
5. Branch lookup must be project-scoped.

---

## Response Payload

### Sample Response

```json
{
  "branchId": "main",
  "branchName": "Main Branch"
}
```

---

## Response Parameters

| Name       | Required | Type   | Description |
|------------|----------|--------|-------------|
| branchId   | True     | String | Unique identifier of the branch. |
| branchName | True     | String | Display name of the branch. |

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 404        | Branch not found in the specified project. |
| 400        | Invalid input parameters. |

---

## Example Use Case

### Get Branch Details

```bash
GET /mbse/api/1.0/branches/main?
projectId=123
```

---

## Implementation Guidelines

- Connector must ensure branch lookup is scoped to the provided `projectId`.
- Branch identifiers must be unique within a project.
- Do not return null response for non-existing branch — explicitly return HTTP `404`.

---

## Design Rationale

This API provides:

- Strict branch validation
- Clear project scoping
- Deterministic behavior for multi-branch systems

It ensures branch-level
