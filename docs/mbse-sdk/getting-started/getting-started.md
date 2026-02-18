# Overview
MBSE SDK REST APIs are used by OpsHub to interact with MBSE connector SDK to read and write data in the MBSE type end system.  
These APIs can be written in any language and hosted anywhere, as long as the OpsHub integration server can access them.

# Gathering the Requirements and Integration Modelling

- First step of connector development is to gather the requirements and do the integration modelling.
- Then check the APIs available in the tool.
  - At least the following APIs should be available in the tool to be integrated with OpsHub MBSE SDK:
    - Get all projects / models / workspaces API
    - Get element, Create element, Update element APIs
    - Query elements or list elements API
      - Or revision APIs such as get all revisions, get elements changed in revisions, get elements at revision, etc.
    - If relations need to be supported
      - Then, there must be an API to get relations of an element and to create relations between elements.

# Start Connector Development

## MBSE SDK APIs
- Refer to **[Build Your Own Connector](mbse-sdk-connector-apis.md)** page for the list of APIs to implement a connector.

### MBSE SDK Bootstrap Package
If an SDK Connector is going to be developed in **Java**,  
a quick start package is available with:
- Basic skeleton of all the APIs to be implemented
- Request and response Java objects for each API
- Sample REST client
- Various utilities

<!-- TODO: Change the link -->
Click **[1.0.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgB2GwvZGsFzTb8G8eOLDsoHAVGOfcyUg0Z-XDYSNM-6ZdY?e=YQ7PWC)** to download the documentation for the MBSE Connector SDK Bootstrap Package.

The bootstrap package can be downloaded from the table below.


## SDK Server Bootstrap Package vs OIM Version Compatibility Matrix

<!-- TODO: Change the link -->

| SDK Server                                                                                                                                                            | OIM Version Range    | Remarks                                                                                |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|----------------------------------------------------------------------------------------|
| [1.0.0 - link will be added shortly]() | \>= 7.218 | Initial version. <br> OIM supports MBSE SDK connector registration from 7.218 onwards. |


# Some Useful SDK Pages
 * [APIs Required for Each Feature](mbse-apis-required-for-each-feature.md)
 * [SDK Best Practices](mbse-sdk-best-practices.md)

