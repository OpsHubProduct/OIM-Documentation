# Passing the Configuration Parameters to MBSE SDK APIs
* OpsHub Integration Manager assumes that Connector MBSE SDK API implementation will be stateless. MBSE SDK is not required to have a database to persist any data(though, if MBSE SDK implementation wants to use a database to store something, they can do it)
* OpsHub Integration Manager will capture all the required parameters at the time of system configuration. OpsHub will pass all these parameters to the connector MBSE SDK APIs in Request Header for each API call.
