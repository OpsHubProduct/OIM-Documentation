## Overview
Returns the connector discovery details.

When registering a connector in OIM, OIM will call this API for each registered MBSE SDK API Base URL to ensure that the URL points to an MBSE SDK implementation. In case of load balancing, you can host the same MBSE SDK connector on multiple servers and register each server URL in OIM. OIM will verify if each registered MBSE SDK API Base URL has the same discovery details, i.e., the same `connectorName` and `connectorVersion`.

## API URI
OpsHub will execute the following API:

```http
GET: /discover
```

## Response Payload

```json
{
  "connectorName": "Rhapsody",
  "connectorVersion": "1.0.0"
}
```

## Response Parameters

| Name | Required | Type | Description                                                                                                                                                                           |
|------|---------|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| connectorName | True | String | Name of the connector implementation. It can be the name of the end system for which the MBSE SDK is implemented.                                                                     |
| connectorVersion | True | String | Version of the connector implementation. Version can be incremented each time a new feature is implemented in MBSE SDK, and it is being used for integration in OIM at the same time. |
