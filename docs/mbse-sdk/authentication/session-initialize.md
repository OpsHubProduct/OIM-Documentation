# Overview
MBSE SDK can use this API to connect to end system. OpsHub will send all the connection details (e.g., URL, username, password, port, host etc.) user specified in integration, that MBSE SDK can use to connect to end system.  

- API will return the parameters which it will need for all subsequent API calls.  
- All the response parameters returned by this, will be passed by OpsHub in subsequent APIs, as Request Headers.  
- When token gets expired, MBSE SDK need to pass the appropriate HTTP status code (Refer to [Error Handling](../getting-started/error-handling.md) page). On receiving this error code, OpsHub will again call initialize API to renew the token.

# Recommendations
- When initialize API is called, all the system configuration details are passed in the request. Connector should do necessary validation for the configuration fields. e.g., If a field's value is expected to be a JSON, the JSON value can be validated in this API call.

# API URI
This is the URI, OpsHub will execute to call this API:


```http
POST: /mbse/api/1.0/initialize/{sdkSessionId}?systemId=<systemId>
```

# Request Payload

```json
[
  {
    "key": "<endSystemUrl>",
    "value": "https://end-system.com",
    "sensitive": false
  },
  {
    "key": "<userName>",
    "value": "user.name",
    "sensitive": false
  },
  {
    "key": "<password>",
    "value": "password",
    "sensitive": true
  },
  {
    "key": "customParam1",
    "value": "param1Value",
    "sensitive": false
  },
  {
    "key": "customParam2",
    "value": "param2Value",
    "sensitive": false
  },
  {
    "key": "suppressNotification",
    "value": "1",
    "sensitive": false
  }
]
```

> **Note**: If Suppress End System Notification is enabled on the Integration Configuration page, the selected option is passed in the request payload using the key suppressNotification. 
> * When set to True, suppressNotification = "1", meaning notifications are suppressed. 
> * When set to False, suppressNotification = "2", meaning notifications will be sent as usual. 
> * For more details, see [**Suppress End System Notification**](../../integrate/integration-configuration.md#suppress-end-system-notification). 

# Request Body

| Name      | Type    | Required | Description |
|-----------|---------|----------|-------------|
| key       | String  | True     | Key will contain name of field input to be taken by end user while creating the System in OpsHub |
| value     | String  | True     | It will contain the value given by the user for that field |
| sensitive | Boolean | True     | Sensitive says if the data is sensitive or not. E.g. password, token will be sensitive |

# Response Payload

```json
[
  {
    "key": "<Authorization>",
    "value": "Bearer fbcf2630-42a1-4094-96db-2ba1d98e1029",
    "sensitive": false
  },
  {
    "key": "<X-endSystemUrl>",
    "value": "https://end-system.com",
    "sensitive": false
  },
  {
    "key": "<X-customParam1>",
    "value": "param1Value",
    "sensitive": false
  }
]
```

# Response Body

| Name      | Type    | Required | Description                                                                                                                                                                                                                                                                                      |
|-----------|---------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| key       | String  | True     | Key can contain any name by which you want to read data later in subsequent APIs. For example, MBSE SDK is authenticating to end system using API token and wants OpsHub to pass this token as part of every subsequent API call, then pass token in value, with any name in key, of your choice |
| value     | String  | True     | It will contain the value that you want to use later                                                                                                                                                                                                                                             |
| sensitive | Boolean | True     | If the data passed is sensitive or not. OpsHub will take care not to log such data in logs                                                                                                                                                                                                       |

