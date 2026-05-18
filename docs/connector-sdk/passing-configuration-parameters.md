---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

- <code class="expression">space.vars.OIM</code> assumes that Connector SDK API implementation will be stateless. SDK is not required to have a database to persist any data (though, if SDK implementation wants to use a database to store something, they can do it).  
- <code class="expression">space.vars.OIM</code> will capture all the required parameters at the time of system configuration. OpsHub will pass all these parameters to the connector SDK APIs in **Request Header** for **each API call**.
