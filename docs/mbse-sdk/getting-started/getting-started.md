# Overview
MBSE SDK REST APIs are used by OpsHub to interact with connector SDK to read and write data in the end system.  
These APIs can be written in any language and hosted anywhere, as long as the OpsHub integration server can access them.

# Gathering the Requirements and Integration Modelling

<!-- TODO: Change the following documents -->
- Refer to the following document to check the required APIs in the end system for implementing a mbse based connector:  
  **[API Recommendation for Connector](https://opshubtrial-my.sharepoint.com/:w:/g/personal/support_opshub_com/EcI_EH7thh1Mh6Qf9c7ry28BqgMe-6Y5zrVDNYDH35iVkA?e=YuIOnx)**

- Refer to the following document and fill in all the details.  
  These details will help you implement a connector based on Connector SDK:  
  **[SDK Technical Analysis Document](https://opshubtrial-my.sharepoint.com/:w:/g/personal/support_opshub_com/Efx9aSynlVJIi0DiO2wObLkB0_tvgddwudtcRKXDHE1Gaw?e=uZH56V)**

# Start Connector Development

## SDK APIs
- Refer to **[Build Your Own Connector](mbse-sdk-connector-apis.md)** page for the list of APIs to implement a connector.

### SDK Bootstrap Package
If an SDK Connector is going to be developed in **Java**,  
a quick start package is available with:
- Basic skeleton of all the APIs to be implemented
- Request and response Java objects for each API
- Sample REST client
- Various utilities

<!-- TODO: Change the link -->
Click **[here](https://opshubtrial-my.sharepoint.com/:b:/g/personal/support_opshub_com/EVms9TRc3Y5Kgby0NIsEvTkBGFnaKbNVUnae2I9fR9EXFA?e=GlNQaH)** to download the documentation for the MBSE Connector SDK Bootstrap Package.

The bootstrap package can be downloaded from the table below.


## SDK Server Bootstrap Package vs OIM Version Compatibility Matrix

<!-- TODO: Change the link -->

| SDK Server  | OIM Version Range    | Remarks                                                                                |
|-------------|----------------------|----------------------------------------------------------------------------------------|
| [1.0.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EvJdBwrcg49MmUBujzlJsN8BTQfy-ZwVjwQz-S0vP8PvcQ?e=7dg12z)     | \>= 7.218 | Initial version. <br> OIM supports MBSE SDK connector registration from 7.218 onwards. |


# Some Useful SDK Pages
 * [APIs Required for Each Feature](mbse-apis-required-for-each-feature.md)
 * [SDK Best Practices](mbse-sdk-best-practices.md)

