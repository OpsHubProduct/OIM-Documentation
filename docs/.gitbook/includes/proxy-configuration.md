# proxy-configuration

{% if "OpsHub Migrator for Microsoft Azure DevOps" === visitor.claims.unsigned.product %}    
To start the <code class="expression">visitor.claims.unsigned.product</code> installer on a machine that is behind a proxy, please perform the following steps:
{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}  
1.
{% endif %}

{% if "OIM" === visitor.claims.unsigned.product %}  
6.
{% endif %}

Open environment configuration from My Computer -> Properties -> Advanced System Settings -> Environment Variables

<div align="center"><img src="../assets/Proxy%201.png" alt="" width="600"></div>

<div align="center"><img src="../assets/Proxy2.png" alt="" width="600"></div>

<div align="center"><img src="../assets/Proxy3.png" alt="" width="600"></div>

{% if "OM4ADO" === visitor.claims.unsigned.product %}  
2.
{% endif %}

{% if "OIM" === visitor.claims.unsigned.product %}  
7.
{% endif %}

Create a new environment variable with the name **"\_JAVA\_OPTIONS"**.

<div align="center"><img src="../assets/Proxy4.png" alt="" width="600"></div>

{% if "OM4ADO" === visitor.claims.unsigned.product %}  
3.
{% endif %}

{% if "OIM" === visitor.claims.unsigned.product %}  
8.
{% endif %}

Set the variable's value as per the format ->\
`-Dhttp.proxyHost= -Dhttp.proxyPort= -Dhttp.nonProxyHosts="localhost|127.0.0.1" -Dhttp.proxyUser= -Dhttp.proxyPassword= -Dhttps=`

| **Attribute**          | **Description**                                                                                                                                                                            |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-Dhttp.proxyHost`     | Proxy server host address                                                                                                                                                                  |
| `-Dhttp.proxyPort`     | Proxy server host port number                                                                                                                                                              |
| `-Dhttp.nonProxyHosts` | Hosts accessible without proxy server                                                                                                                                                      |
| `-Dhttp.proxyUser`     | User name to access proxy server                                                                                                                                                           |
| `-Dhttp.proxyPassword` | Password for the provided username to access proxy server                                                                                                                                  |
| `-Dhttps`              | <p>If proxy server is hosted over HTTPS, then set this parameter as <code>"true"</code> else <code>"false"</code>.<br>This attribute is not mandatory. Default is <code>"false"</code></p> |

**For example:**\
`-Dhttp.proxyHost='00.00.00.00' -Dhttp.proxyPort='8080' -Dhttp.nonProxyHosts="localhost|127.0.0.1" -Dhttp.proxyUser='username' -Dhttp.proxyPassword='password' -Dhttps=false`

In the above example:\
ProxyIP → `00.00.00.00`, Proxy Port → `8080`, Proxy User Name → `username`, Proxy Password → `password`

<div align="center"><img src="../assets/Proxy5.png" alt="" width="600"></div>

{% if "OM4ADO" === visitor.claims.unsigned.product %}  
4. Save all the changes.
{% endif %}

{% if "OIM" === visitor.claims.unsigned.product %}  
9. Save all the changes and restart the <code class="expression">visitor.claims.unsigned.product</code> Service.
{% endif %}

{% if "OIM" === visitor.claims.unsigned.product %}  
10. Test the proxy by opening service URL \*\*http://:/TFSService\*\* in browser. Now check the connection by trying to create mapping.
{% endif %}

> **Note**: Even after performing all these steps, if you are still unable to connect, then please check the proxy credentials given in
>
> {% if "OM4ADO" === visitor.claims.unsigned.product %}  
> Step 3
> {% endif %}
>
> {% if "OIM" === visitor.claims.unsigned.product %}  
> Step 8
> {% endif %}
>
> and
>
> {% if "OM4ADO" === visitor.claims.unsigned.product %}  
> restart your installer.
> {% endif %}
>
> {% if "OIM" === visitor.claims.unsigned.product %}  
> restart the <code class="expression">visitor.claims.unsigned.product</code> Service.
> {% endif %}
