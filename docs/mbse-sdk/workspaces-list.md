# Overview
Get the workspaces from the end system that the integration user has access to.

>**Note**: Return the empty list if the end system does not have the Workspaces' structure.

# API URI
This is the URI OpsHub will execute to call this API:

```bash
GET: /workspaces?
startIndex=<startIndex>
maxResults=<maxResults>
```

# URI Parameters

| Name        | In    | Required | Type    | Description                                                                               |
|------------|-------|----------|---------|-------------------------------------------------------------------------------------------|
| startIndex | Query | True     | Integer | Start index from which list of workspaces should be returned                              |
| maxResults | Query | True     | Integer | Maximum number of workspaces to be returned by custom connector, starting from startIndex |

# Response Payload

```json
[
  {
    "id": "unique identifier",
    "name": "project name",
    "parentWorkSpaceId": "parent workspace id"
  }
]
```

| Name              | Type            | Required | Description                                                                                                   |
|-------------------|----------------|----------|---------------------------------------------------------------------------------------------------------------|
| id                | Integer or String | True     | Id or internal name of the workspace                                                                          |
| name              | String          | True     | Display name of the workspace                                                                                 |
| parentWorkSpaceId | String          | False    | If end system supports workspace hierarchy, set the id or internal name of the direct parent workspace |

# Examples

## Flat workspace list

**Example 1:**

```json
[
  {
    "id": "1",
    "name": "Sample Workspace",
    "parentWorkSpaceId": ""
  },
  {
    "id": "2",
    "name": "Demo Workspace",
    "parentWorkSpaceId": ""
  }
]
```
## Example 2

```json
[
  {
    "id": "SAMP",
    "name": "Sample Workspace",
    "parentWorkSpaceId": ""
  },
  {
    "id": "DEMO",
    "name": "Demo Workspace",
    "parentWorkSpaceId": ""
  }
]
```
## Workspace hierarchy

```json
[
  {
    "id": "root",
    "name": "Main Child Workspace",
    "parentWorkSpaceId": "Main Workspace"
  },
  {
    "id": "1",
    "name": "Sample Workspace",
    "parentWorkSpaceId": "Demo Workspace"
  },
  {
    "id": "2",
    "name": "Demo Workspace",
    "parentWorkSpaceId": "1"
  },
  {
    "id": "3",
    "name": "Trial Workspace",
    "parentWorkSpaceId": "1"
  }
]

```

