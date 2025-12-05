**Common**
* Impersonation is not supported due to TFS/ADO API limitation.
* These artifacts do not have history, attachment, comments and inline image, as they will not be synced.

**Entity Specific:**
Following are the limitations and behaviors specific to the individual entities in addition to the common:

**Service Connection Entity**

**Known Behaviour and Limitations:**
  * After a successful synchronization of the Service Connection, you need to enter the password manually in the target project as Microsoft API does not expose this sensitive data due to security concerns.
  * Service Connections of type **Azure Resource Manager** cannot be synchronized from **Azure DevOps Server** to **Azure DevOps Services**.
    * Reason: There is a template mismatch in Azure Resource Manager between Azure DevOps Services (cloud) and Azure DevOps Server (TFS). Due to these template differences and API limitations, this service connection will not synced from ADO Cloud to TFS.

**Agent Pool Entity**

**Known Behaviour and Limitations:**
  * By default, <code class="expression">space.vars.SITENAME</code> synchronizes project-level Agent Pools [the collection level pools which are associated with projects].
  * To synchronize collection-level Agent Pools as well, set the “Collection Level” option to Yes, at the integration of Agent Pool as shown in the below image:
    <p align="center">
      <img src="../../assets/AgentPoolCollectionLevel.png"/>
    </p>
  * When this option is enabled, both project-level and collection-level Agent Pools will be synchronized.


