## Overview
Deletes an attachment.

## API URI
This is the URI OpsHub will execute to call this API:

```bash
DELETE: entities/{entityTypeId}/{entityId}/attachments? 
attachmentId={attachmentId}& 
projectId={projectId}&
attachmentType={attachmentType}&
typeItemId={typeItemId}
```

## URI Parameters

| Name           | In    | Required | Type   | Description                                                                                                                                                                                    |
|----------------|-------|----------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| entityTypeId    | path  | True     | String | ‘id’ of entity type for given entity id                                                                                                                                                        |
| entityId        | path  | True     | String | ‘id’ of the entity in which attachment to be deleted                                                                                                                                           |
| attachmentId    | path  | True     | String | Id of the attachment that needs to be deleted                                                                                                                                                  |
| projectId       | query | True     | String | Project in which the given entity exists                                                                                                                                                       |
| attachmentType | query | False    | String | Name of the field from which the attachment is to be deleted.<br>For example, if the attachment is to be deleted from 'Steps' field,<br>attachmentType="Steps"                                 |
| typeItemId     | query | False    | String | Id of the item from which the attachment is to be deleted.<br>For example, if the attachment is to be deleted from step 1 of 'Steps' field, provide id of step 1,<br>typeItemId="10409526" |

## Request Payload
This API does not require a request body. Only HTTP status `204` is returned on successful deletion.

