# API Name
**Link – Delete**

## Overview
Deletes links between two entities from the end system.


## API URI
```bash
POST: /entities/{entityTypeId}/{entityId}/links/delete?projectId=<projectId>
```

## URI Parameters

| Name         | In     | Required | Type   | Description |
|--------------|--------|----------|--------|-------------|
| entityTypeId | path   | True     | String | `id` of the entity type for the given entity id. |
| entityId     | path   | True     | String | `id` of the entity in which links need to be deleted. |
| projectId    | query  | True     | String | Project in which the given entity exists. |


## Request Payload

| Name      | Required | Type   | Description |
|-----------|----------|--------|-------------|
| linkType  | True     | String | The type of link for which links are to be deleted. Example: `Parent`, `Child`, `Related`. <br><br>**If connector supports rank:**<br>If `links.rank.orderType` from [Entity Type – Get](entity-type-get.md) API is either `HIERARCHY_SINGLE` or `HIERARCHY_MULTIPLE`, handle additional link types `Hierarchy Parent` and `Hierarchy Child`. |
| links     | True     | List   | List of links to be deleted. Each link in the list has the following structure:<br><br> [<br> { `"<linkedEntityIdField>"`: "The name will be the field name in which entity of the linked entity will come, and the value will be the entity id to which entityId coming in request URI need to be deleted", <br>  `"<linkedEntityTypeField>"`: "The name will be the field name in which entity type of linked entity will come, and the value will be the entity type of linked entity id that needs to be deleted" <br> } <br>] |

**Example**
```json
{
  "linkType": "Parent",
  "links": [
    {
      "linkedEntityId": "1234",
      "linkedEntityType": "Task"
    },
    {
      "linkedEntityId": "5678",
      "linkedEntityType": "Story"
    }
  ]
}
```

## Response Payload
Only HTTP status `204`.



