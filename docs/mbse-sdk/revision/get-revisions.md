# API Name
API Name: Revisions – Get

---

# Overview

This API returns the list of revisions for a given project.

MBSE Core uses this API for:

- Polling revision history
- Incremental synchronization
- Identifying changes within a time window
- Fetching revisions in chronological order

Connector implementation **must**:

- Sort revisions strictly based on `revisionTime`
- Implement pagination even if the end system does not support it natively
- Respect `pageNumber` and `pageSize` in all cases
- Apply time filtering (`afterTime`, `beforeTime`) if supported by the end system
- If time filtering is not supported, return complete data and allow MBSE Core to filter

This API does **not** support `nextPageLink`. Pagination is strictly controlled using `pageNumber` and `pageSize`.

---

## API URI

```bash
GET: /mbse/api/1.0/revisions
    ?projectId={projectId}
    &elementTypeIds={elementTypeIds}
    &branchId={branchId}
    &afterTime={afterTime}
    &beforeTime={beforeTime}
    &pageNumber={pageNumber}
    &pageSize={pageSize}
    &orderByDirection={ASC|DESC}
```

---

## URI Parameters

| Name             | Mandatory | Type          | Description |
|------------------|-----------|--------------|-------------|
| projectId        | True      | String       | ID of the project for which revisions need to be fetched. |
| elementTypeIds   | True      | List<String> | List of element type IDs defined in `element-types` JSON configuration. Only revisions affecting these element types must be returned. |
| branchId         | False     | String       | ID of the branch from which revisions need to be retrieved. If omitted, default branch behavior of the end system should apply. |
| afterTime        | False     | String       | Time filter in format `YYYY-MM-dd'T'HH:mm:ss.SSSX`. Returns revisions updated strictly after this time. If end system does not support filtering, return full data and MBSE Core will filter. |
| beforeTime       | False     | String       | Time filter in format `YYYY-MM-dd'T'HH:mm:ss.SSSX`. Returns revisions updated strictly before this time. If end system does not support filtering, return full data and MBSE Core will filter. |
| pageNumber       | True      | Integer      | 0-based page index indicating which page of results to return. |
| pageSize         | True      | Integer      | Number of revisions to return per page. |
| orderByDirection | True      | String       | Sorting direction based on `revisionTime`. Possible values: `ASC` (oldest first) or `DESC` (latest first). |

---

## Behavior Rules

1. Revisions must be sorted strictly by `revisionTime`.
2. `revisionTime` is the primary and authoritative sorting field.
3. Pagination is mandatory. Connector must:
    - Apply `pageNumber` and `pageSize`
    - Return only the requested page of results
    - Implement pagination logic even if the end system does not support it natively.
4. If both `afterTime` and `beforeTime` are provided, return revisions such that:

   afterTime < revisionTime < beforeTime

5. If the end system does not support:
    - Time filtering → return complete data and allow MBSE Core to filter.
    - Branch filtering → apply default branch behavior.

6. Only revisions affecting the provided `elementTypeIds` must be returned.
7. This API must not return element-level change details. It only returns revision metadata.

---

## Response Payload

> Note: This is a sample response. Actual revision identifiers and metadata depend on the end system implementation.

```json
{
  "revisions": [
    {
      "revisionId": "rev_20260214_001",
      "parentRevisionId": "rev_20260213_004",
      "revisionTime": "2026-02-14T10:15:32.456Z",
      "author": "john.doe",
      "comment": "Updated Block definition and fixed constraint relations."
    },
    {
      "revisionId": "rev_20260214_002",
      "parentRevisionId": "rev_20260214_001",
      "revisionTime": "2026-02-14T11:02:18.123Z",
      "author": "jane.smith",
      "comment": "Added new Requirement and linked to existing System Block."
    }
  ]
}
```

---

## Response Parameters

| Name      | Required | Type         | Description |
|-----------|----------|-------------|-------------|
| revisions | True     | List<Object> | List of revisions matching the provided filters and pagination parameters. |

### Revision Object

| Name             | Required | Type   | Description |
|------------------|----------|--------|-------------|
| revisionId       | True     | String | Unique identifier of the revision in the end system. |
| parentRevisionId | False    | String | Identifier of the parent revision. Used to represent revision lineage or commit chain. |
| revisionTime     | True     | String | Timestamp when the revision was created. Format: `YYYY-MM-dd'T'HH:mm:ss.SSSX`. |
| author           | True     | String | Username or identifier of the user who created the revision. |
| comment          | False    | String | Revision message or comment associated with the revision. |

---

## Deterministic Ordering Requirement

Connector must ensure deterministic ordering of revisions.

If multiple revisions have identical `revisionTime`, connector should apply a secondary sort using `revisionId` to maintain consistent ordering across pages.

---

## Example Use Cases

### 1) Polling Revisions After a Given Time

```bash
GET /mbse/api/1.0/revisions?
projectId=123
&elementTypeIds=Block,Requirement
&afterTime=2026-02-14T08:00:00.000Z
&pageNumber=0
&pageSize=100
&orderByDirection=ASC
```

### 2) Fetch Latest Revisions

```bash
GET /mbse/api/1.0/revisions?
projectId=123
&elementTypeIds=Block
&pageNumber=0
&pageSize=50
&orderByDirection=DESC
```

---

## Implementation Notes for Connector Developers

- Revision granularity must align with the end system’s commit model.
- If multiple element changes are grouped under one revision in the end system, return that revision only once.
- Do not include element change details in this API.
- Element-level changes must be retrieved using corresponding element-change APIs.
- Pagination logic must be implemented at connector level if end system lacks native support.
