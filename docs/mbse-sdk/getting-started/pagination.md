---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

- For each list API, OpsHub will send **startIndex** and **maxResults**.  
  - MBSE SDK API needs to define the maximum records (**maxResults**) that can be fetched in one page in [**server-info**](../metadata/server-info.md) API.  
- OpsHub will take care of looking through the results and calling list API again, if required, for the next page.  
- MBSE SDK API should only give <code class="expression">space.vars.OIM</code> the result for the given **startIndex** and **maxResults**.
