# API Name

API Name: Branch – Create

---

# Overview

This API creates a new branch within a given project.

Branch name selection is delegated to the connector implementation because:

- Branch naming rules vary across end systems.
- Some systems enforce strict naming constraints.
- Some systems automatically append suffixes for uniqueness.
- Some systems reject duplicate branch names.

Connector responsibility:

- Generate a unique branch name compliant with end system constraints.
- Preferably use a timestamp-based strategy to ensure uniqueness.
- Call the end system API to create the branch in the specified project.
- Return created branch details.
- If branch creation fails, return appropriate error response.

---

## API URI

```bash
POST: /mbse/api/1.0/branches
    ?projectId={projectId}
```

---

## URI Parameters

| Name      | Mandatory | Type   | Description |
|-----------|-----------|--------|-------------|
| projectId | True      | String | ID of the project in which the branch needs to be created. |

---

## Behavior Rules

1. Branch must be created within the context of the given `projectId`.
2. Connector must:
    - Generate a branch name compliant with end system rules.
    - Ensure branch name uniqueness.
3. Recommended approach:
    - Use timestamp-based naming strategy (e.g., `branch_YYYYMMddHHmmss`).
4. The API must return the created branch details.
5. If branch creation fails:
    - Return appropriate HTTP error code.
6. Connector must not return a null response.

---

## Response Payload

### Sample Response

```json
{
  "branchId": "branch_20260214123045",
  "branchName": "branch_20260214123045"
}
```

---

## Response Parameters

| Name       | Required | Type   | Description |
|------------|----------|--------|-------------|
| branchId   | True     | String | Unique identifier of the newly created branch. |
| branchName | True     | String | Display name of the branch. |

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid project ID or invalid request. |
| 404        | Project not found. |
| 409        | Branch creation conflict (if applicable). |
| 500        | Internal server error during branch creation. |

---

## Example Use Case

### Create New Branch

```bash
POST /mbse/api/1.0/branches?
projectId=123
```

---

## Implementation Guidelines

- Connector must sanitize branch name according to end system rules.
- Avoid hardcoding branch names.
- Prefer deterministic timestamp-based naming for traceability.
- Ensure created branch belongs strictly to provided project.
- Return branch details exactly as created in end system.

---

## Design Rationale

This API keeps branch naming logic flexible and system-aware.

By delegating naming to the connector:

- The MBSE layer remains system-agnostic.
- Integration remains portable across multiple modeling tools.
- Naming conflicts are handled locally by connector logic.

This design ensures consistent behavior across heterogeneous MBSE systems.
