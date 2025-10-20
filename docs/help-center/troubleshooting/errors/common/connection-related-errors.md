# Description

## Types of Connection Errors

* **End point not found/HTTP – 404 Errors**  
  * Such errors occur when configured URL is entered during system configuration in an incorrect manner/format. To ensure the URL is entered correctly, admin must verify the configured URL within the end point configuration. Refer to the tool-tip for the expected URL format and other requisite details in the system configuration documentation.  
  * When the end point URL is behind a proxy, it is possible that the admin then might need to setup proxy parameters in [Proxy Setting](../../../../manage/administrator/proxy-setting.md).

* **Authentication/Authorization Errors**  
  * These types of errors come when the username or password entered in the system is wrong or does not have sufficient privileges to perform required operations. In this case, admin is required to verify configured username and password and validate required permissions against the pre-requisite section of the respective system.

# Causes & Solutions

There are couple of reasons due to which connection-related error(s) might occur. Given below are the possible reasons and solutions for the given errors.

## Error message contains one of following sub statements:
* Peer not authenticated, PKIX path building failed, unable to find valid certification path to requested target.  
  * Such error occurs when the end system is configured over Secure Socket Layer (SSL). In this case, user needs to import the site certificate in Java Key Store used by OIM. Using the steps given in [SSL Certificate Configuration](../../../../getting-started/installation.md#ssl-certificate-configuration), certificate can be imported. This will fix the error.

* **Host not reachable/accessible**  
  * Configured system is not reachable from the machine where synchronization platform is installed. To validate, user needs to trigger ping command on console from the server machine, ”“ping hostname -t””. If the command results into errors such as request timed out (continuous), unknown host, destination host unreachable then it means that the system is not reachable from the machine where OIM is installed. In such cases, user can check Proxy Setting or try to load the end system in the browser to check whether connectivity is present or not. If the system loads in the web browser then there are chances that system is behind the proxy server, user needs to follow the steps mentioned in [Proxy Setting](../../../../manage/administrator/proxy-setting.md).

* **Intermediate request timed out in ping command’s response**  
  * This means, system is reachable but intermediate network packets/frames are dropped during the transit. For synchronization tool to work smoothly, network should be reliable so that it does not drop packets/frames frequently. Such situations can be debugged and fixed with the help of network administrator team.

* **Reverse Proxy setup**  
  * Sometimes reverse proxies/gateways are configured within the network infrastructure in a manner that requests that run for more than few seconds are automatically dropped by the proxy configuration. In such scenarios, it is important to ensure that user configures enough threshold for http request to complete its execution on end point’s server.  
    * In this particular case, error comes at specific time duration (as per configuration in reverse proxy). Network admin team member needs to debug and fix these types of issues.

* **Server closes connection/server timeout**  
  * This type of error usually occurs in very rate cases, especially when end point’s server parameters are badly configured. If server-side timeout is configured very low then requests might be timed out by the server itself. In such cases, endpoint server’s timeout parameter is required to be tuned such that requests can be executed within reasonable time limit.

* **Connectivity issue with VPN configuration**  
  * There are very less chances but sometimes VPN might restrict connection to the end system. In case system doesn’t require VPN access, then user can stop the VPN and try to connect with the end system to further analyze this type of error.


