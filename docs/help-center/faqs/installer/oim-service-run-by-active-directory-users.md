## Description

{% if "OM4ADO" === visitor.claims.unsigned.product %}
Can the <code class="expression">space.vars.OM4ADO</code> Service be run by Active Directory users? If yes, what are the permissions required to run it?
{% endif %}
{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}
Can the OpsHub Server Service be run by Active Directory users? If yes, what are the permissions required to run it?
{% endif %}

## Solution
{% if "OM4ADO" === visitor.claims.unsigned.product %}   
OpsHub Migrator for Microsoft Azure DevOps Service can be run by a standard Windows login user as well as an Active Directory user with admin privileges.
{% endif %}
{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}  
OpsHub Server Service can be run by a standard Windows login user as well as an Active Directory user with admin privileges. 
{% endif %} 