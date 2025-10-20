# Description

When user encounters OH-Micro Focus ALM/QC-012651, then following error message will appear:

'OH-Micro Focus ALM/QC-012651 : Rest request processing Error : `<status_code>` `<name of the status code>` for the request `<request URL>`'

**Example:**

OH-Micro Focus ALM/QC-012651 : Rest request processing Error : 403 Bad Request for the request http://10.13.28.82:8181/qcbin/authentication-point/authenticate

# Cause

* This error may occur when the user mentioned in the system configuration form is not present as a project user in Micro Focus ALM/QC for the project being used in the integration.

# Solution

* To add the user as a **Project User** in Micro Focus ALM/QC, please refer: [Add a project user in a project](../../../../connectors/micro-focus-alm-qc.md#add-project-user-in-project)

