## Description

Where to find the logs generated during <code class="expression">visitor.claims.unsigned.product</code> installation?

Logs generated during <code class="expression">visitor.claims.unsigned.product</code> installation are useful in identifying the reason for failure (if any).

## Solution

<code class="expression">space.vars.OIM</code> installation progress gets logged in an `Install.log` file. It contains details of all the steps performed in the process, along with the details of failures (if any).  
This file is located under the 'logs' folder in <code class="expression">space.vars.OIM</code> installation path.

For example:

Operating System: **Windows**  
{% if "OM4ADO" === visitor.claims.unsigned.product %}  
- Installation Path: `C:\Program Files\OM4ADO`  
- Location of log file: `C:\Program Files\OM4ADO\logs\Install.log`  
{% endif %}  
{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}  
- Installation Path: `C:\Program Files\OpsHub`  
- Location of log file: `C:\Program Files\OpsHub\logs\Install.log`  

Operating System: **Linux**  

- Installation Path: `/usr/local/OpsHub`  
- Location of log file: `/usr/local/OpsHub/logs/Install.log`  
{% endif %}
