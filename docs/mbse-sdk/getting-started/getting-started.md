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

The bootstrap package can be downloaded from the compatibility matrix given in [Developer Notes](../developer-notes.md).

# Some Useful SDK Pages
 * [APIs Required for Each Feature](mbse-apis-required-for-each-feature.md)
 * [SDK Best Practices](mbse-sdk-best-practices.md)

