---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Description

This describes how <code class="expression">space.vars.OIM</code> makes connection to ServiceNow.

## Solution

Currently for ServiceNow integration only 'Basic authentication' is supported.  
A user name and password combination is required to access the ServiceNow REST API.
