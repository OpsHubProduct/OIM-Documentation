# Overview

* In many real-world integrations, a single entity type in the source system may need to synchronize with different entity types in the target system based on the value of a specific field — such as Request Type, Category, or Type.

* Even though the source entity type remains the same, its business means changes when that field’s value changes. In such cases, the target entity type should update automatically without creating duplicates, ensuring both systems stay consistent.

This need typically arises when:

* The number of entity types differs between the source and target systems.

* A classification or partitioning field determines how the entity should behave (e.g., Bug, Feature Request, Change Request).

* Entities are created from both systems, and entity type changes must remain synchronized in both directions.

## Handling Rule-Based and Duplicate Configuration

If your configuration includes both **convertible** and **duplicate** entity types — for example, some entities that can convert into each other (*Bug ↔ Story ↔ Epic*) and others that should remain as duplicates (*Task*) — follow the steps below to avoid unexpected behavior.

| **Source Entity Type** | **Target Entity Type(s)** | **Purpose** |
|-------------------------|---------------------------|--------------|
| Bug                    | Bug / Story / Epic         | Conversion between related types |
| Bug                    | Task                       | Duplicate creation |

* Do **not** use the same source–target system pair for both rule-based and duplicate configurations.
* Create a **separate system** for the duplicate configuration.  
  This separation ensures that conversion logic applies only to convertible entity types and does not affect duplicate entities.

## Know Behaviors
* If entity matched multiple rules and no rules, then the sync will be failed with below-mentioned processing failure
    * Example 1: Multiple Routing Rule Match:
        * Row1: `{"condition":"OR","criterias":[{"condition":"EQUALS","field":"type","value":"Bug"},{"condition":"EQUALS","field":"priority","value":"Low"}]}`
        * Row2: `{"condition":"OR","criterias":[{"condition":"EQUALS","field":"type","value":"Feature"},{"condition":"EQUALS","field":"priority","value":"High"}]}`
        * The entity read from the end system has `type = 'Feature'` and `priority = 'Low'`, in this case, multiple routing rules are matched.
    * Example 2: No Routing Rule Match
        * Row1: `{"condition":"OR","criterias":[{"condition":"EQUALS","field":"type","value":"Bug"},{"condition":"EQUALS","field":"priority","value":"Low"}]}`
        * Row2: `{"condition":"OR","criterias":[{"condition":"EQUALS","field":"type","value":"Feature"},{"condition":"EQUALS","field":"priority","value":"High"}]}`
        * The entity read from the end system has `type = 'Story'` and `priority = 'Medium'`, in this case, no routing rule is matched.

## Routing Rules Configuration Guidelines

Follow these guidelines when configuring the **Routing Criteria** and **Routing Query** in the **Routing Criteria Settings** section:

* Configure **routing rules** for every row, otherwise you will not be able to save the integration.
* Write the routing query in the [OpsHub Query Format](opshub-query-format.md).

* Make sure the **Default Values** in the **Routing Criteria Field Values** table match the routing criteria.
    * Each value in the field values table must be a valid subset of the defined routing criteria.
    * **Example:** If the routing criteria is `{"condition": "IN", "field": "priority", "values": ["High", "Medium"]}`, then only *High* and *Medium* can be used as default values for *priority*.

* Do **not** map the fields in the mapping used in the routing criteria query.
    * Example: If the routing criteria query uses the `priority` field, it should not be mapped in the sync direction from the N-side configuration to the 1-side configuration, as <code class="expression">space.vars.SITENAME</code> automatically manages the field's value based on the defaults defined in the Routing Criteria Field Values table.
* Use the **same field set** across all rows in a rule-based configuration.
    * Example: If one row in a rule-based configuration uses the `priority` field in its routing query, then all other rows in that configuration must also use only the `priority` field in their routing queries.

* Keep all **routing rules independent** across rows.
    * Example: If one row in a rule-based configuration uses the routing criteria
      `{"condition": "IN", "field": "priority", "values": ["High", "Medium"]`}, then another row in the same configuration **cannot** use`{"condition": "IN", "field": "priority", "values": ["High", "Low"]}`. Each row must define a distinct and non-overlapping routing rule.

* Do **not** use routing-based configuration if duplication is expected in the target.
    * If one source entity needs to stay in sync with multiple target entity types at the same time, avoid rule-based routing.  
      Under rule-based routing, a source entity can sync with only one target entity type at a time — based on the rule it matches.

# default route Configuration Guidelines

Follow these guidelines when configuring the **default route**:

* Only one default route can be configured, within a given rule-based configuration.
* The default route is applied only when no routing criteria match for an incoming entity.
* Changes to the default route can impact previously synchronized entities.
    * When modified, entities that were synchronized due to default route may undergo entity type conversion during subsequent synchronization.
* Disabling the default route will result in synchronization failures for incoming entities where no routing criteria match.

# Example Use Case

Consider a source system where all items are created as a Request, and the field **requestType** determines the entity type to be created in the target.

| **requestType Value**  | **Target Entity Type** |
|------------------------|------------------------|
| Bug                    | Bug                    |
| Feature Request        | Feature                |
| Change Request         | Change Request         |    

**Typical Behavior:**

* When the source Request has requestType = Bug, it is synchronized as a Bug in the target system.
* If the requestType changes to Feature Request, the previously synced Bug is automatically converted to a Feature Request — without creating duplicates.
* If the entity type changes on the target side, the requestType field in the source system updates automatically to stay aligned.

# Default Route Use Case

In integrations where routing criteria determine the target entity type,
there may be scenarios where incoming entities do not match any configured conditions.
The default route ensures such entities are still processed by assigning a fallback target entity type.

Consider a source system where all items are created as a Request, and the field **requestType** determines the entity type to be created in the target (as per the above example use-case)

Integration Configuration with default route

| **Source Entity Type**  | **Target Entity Type** | **Routing Criteria**              | **default route**      |     
|------------------------|-------------------------|-----------------------------------|------------------------|
| Request                | Bug                     |   requestType = Bug               |    false               |
| Request                | Feature                 |   requestType = Feature Request   |    true                |
| Request                | Change Request          |   requestType = Change Request    |    false               |

**Behavior with default route Configured**
* When a source Request has requestType = Story (or any value not matching configured criteria), no explicit routing criteria is satisfied.
* In such cases, the *default route* is applied for the synchronization, For example, for requestType = Story, the target entity type will be Feature (as per the above configuration).

**Behavior When default route is Changed**

* Continuing the above scenario, a Request with requestType = Story is initially synchronized as a Feature.
* If the default route is changed to requestType = Bug route.
  * On the next synchronization, the existing target entity will be converted from Feature to Bug.
* **Warning** : Changing default route will change the entity type of all records synchronized via the default route in the next sync cycle.

**Behavior When default route is Disabled**

* If the default route is disabled and an entity does not match any routing criteria:
  * The synchronization will fail with the error message: "OpsHub-020604: No routing criteria matched the provided entity values. Review the currently configured routing criteria: {currently configured criteria}"

<code class="expression">space.vars.SITENAME</code> allows seamless conversion when the routing field value changes and automatically updates the corresponding target entity type. It also ensures that when updates flow in the reverse direction, the source field value is adjusted accordingly, maintaining complete bidirectional consistency. For more details about configuration, refer to this section: [Routing Rules Configuration](integration-configuration.md#rule-based-routing).
