# Integration-Level Criteria Configuration (MBSE)

Integration-Level Criteria Configuration allows administrators to define element-level filters that determine which records are eligible for synchronization in an MBSE integration.

These criteria are evaluated after [package-level filtering](package-selection-criteria.md) (if configured) and ensure that only elements matching the specified conditions are processed.

---

## Overview

Integration-level criteria are defined using a structured JSON configuration.
The criteria support simple equality checks and list-based value matching.

Only elements that satisfy all configured criteria conditions are synchronized.

---

## Supported Conditions

| Condition  | Description                                                                     |
|------------|---------------------------------------------------------------------------------|
| `EQUALS`   | Matches elements where the specified field exactly equals the given value.      |
| `IN`       | Matches elements where the field value exists within a provided list of values. |
| `AND`      | Combines multiple criteria conditions (logical AND only).                       |

---
> **Note:** `OR` conditions are not supported.

------------------------------------------------------------------------

## Criteria Format

The configuration must be provided as a JSON array.

### Example: Single Field (EQUALS)

``` json
[
  {
    "field": "Name",
    "condition": "EQUALS",
    "value": "Meeting Criteria"
  }
]
```

---

### Example: Multiple Values (IN)

``` json
[
  {
    "field": "Status",
    "condition": "IN",
    "values": ["Open", "In Progress"]
  }
]
```

---

### Example: Multiple Root Criteria (Implicit AND)

When multiple criteria objects are provided at the root level, they are treated as a logical AND.

``` json
[
  {
    "field": "Name",
    "condition": "EQUALS",
    "value": "TestName"
  },
  {
    "field": "Status",
    "condition": "EQUALS",
    "value": "Open"
  }
]
```

Both conditions must be satisfied for the element to be synchronized.

---

### Example: Nested AND Condition

``` json
[
  {
    "condition": "AND",
    "criterias": [
      {
        "field": "Name",
        "condition": "EQUALS",
        "value": "Valid Name"
      },
      {
        "field": "Priority",
        "condition": "EQUALS",
        "value": "P1"
      }
    ]
  }
]
```

Nested criteria are flattened and applied using AND logic.

---

## Evaluation Logic

During synchronization:

1.  The criteria configuration is parsed.
2.  Field-value pairs are extracted.
3.  Each element is evaluated.
4.  An element is synchronized only if **all criteria conditions match**.

### Matching Rules

-   For `EQUALS`, the element field value must match exactly.
-   For `IN`, the element field value must exist in the defined list.
-   Multiple criteria are evaluated using AND logic.
-   If any condition fails, the element is excluded.

---

## Validation Rules

The following validations are enforced:

-   Criteria JSON must be valid.
-   `EQUALS` must include a non-null `value`.
-   `IN` must include a non-null `values` list.
-   `AND` must include a non-null `criterias` array.
-   `OR` is not supported.
-   Unsupported operators result in configuration errors.

Invalid configurations result in runtime validation errors during
criteria extraction.

---

## Interaction with Package Selection Criteria

When both Package Selection Criteria and Integration-Level Criteria are
configured:

1.  Package Selection Criteria filters elements by package.
2.  Integration-Level Criteria further filters those elements by field
    values.

Only elements satisfying both filters are synchronized.

---

## Behavior Notes

-   Criteria are evaluated per element type.
-   All configured conditions must match (logical AND).
-   If no criteria are defined, all elements (subject to other configuration filters) are eligible for synchronization.
-   Criteria apply only to elements included in the integration configuration.

---

## Best Practices

-   Keep criteria simple and deterministic.
-   Use `IN` for controlled status-based filtering.
-   Avoid deeply nested criteria structures unless required.
-   Validate JSON structure before saving configuration.
-   Test synchronization after updating criteria to confirm expected behavior.

---

## Example Use Case

Synchronize only:

-   Requirements with Status = "Approved"
-   Priority = "High"

``` json
[
  {
    "field": "Status",
    "condition": "EQUALS",
    "value": "Approved"
  },
  {
    "field": "Priority",
    "condition": "EQUALS",
    "value": "High"
  }
]
```
