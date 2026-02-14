# Overview
Get the projects from the end system that the integration user has access to.  

>**Note**: Return the `OH_NO_PROJECT` if the end system does not have the Projects' structure.  

# API URI
This is the URI OpsHub will execute to call this API:  

```bash
GET: /mbse/api/1.0/projects?
    startIndex=<startIndex>
    maxResults=<maxResults>
```

# URI Parameters

| Name        | In    | Required | Type    | Description |
|------------|-------|----------|---------|-------------|
| startIndex | Query | True     | Integer | Start index from which list of projects should be returned |
| maxResults | Query | True     | Integer | Maximum number of projects to be returned by custom connector, starting from startIndex |

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

| Name              | Type            | Required | Description                                                                                                    |
|-------------------|----------------|----------|----------------------------------------------------------------------------------------------------------------|
| id                | Integer or String | True     | Id or internal name of the project                                                                             |
| name              | String          | True     | Display name of the project                                                                                    |
| parentWorkSpaceId | String          | False    | If end system supports workspace-project hierarchy, set the id or internal name of the direct parent workspace |

# Examples

## Flat project list

**Example 1:**

```json
[
  {
    "id": "1",
    "name": "Sample Project",
    "parentWorkSpaceId": ""
  },
  {
    "id": "2",
    "name": "Demo Project",
    "parentWorkSpaceId": ""
  }
]
```
## Example 2

```json
[
  {
    "id": "SAMP",
    "name": "Sample Project",
    "parentWorkSpaceId": ""
  },
  {
    "id": "DEMO",
    "name": "Demo Project",
    "parentWorkSpaceId": ""
  }
]
```
## Workspace-Project hierarchy

```json
[
  {
    "id": "1",
    "name": "Main Project",
    "parentWorkSpaceId": "ws-1"
  },
  {
    "id": "2",
    "name": "Sample Project",
    "parentWorkSpaceId": "ws-1"
  },
  {
    "id": "3",
    "name": "Demo Project",
    "parentWorkSpaceId": "ws-2"
  },
  {
    "id": "4",
    "name": "Trial Project",
    "parentWorkSpaceId": "ws-2"
  }
]

```

