# Overview

* In many real-world integrations, a single entity type in the source system may need to synchronize with different entity types in the target system based on the value of a specific field — such as Request Type, Category, or Type.

* Even though the source entity type remains the same, its business means changes when that field’s value changes. In such cases, the target entity type should update automatically without creating duplicates, ensuring both systems stay consistent.

This need typically arises when:

* The number of entity types differs between the source and target systems.

* A classification or partitioning field determines how the entity should behave (e.g., Bug, Feature Request, Change Request).

* Entities are created from both systems, and entity type changes must remain synchronized in both directions.

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
The Default Route ensures such entities are still processed by assigning a fallback target entity type.

Consider a source system where all items are created as a Request, and the field **requestType** determines the entity type to be created in the target (as per the above example use-case)

Integration Configuration with Default Route

| **Source Entity Type**  | **Target Entity Type** | **Routing Criteria**              | **Default Route**      |     
|------------------------|-------------------------|-----------------------------------|------------------------|
| Request                | Bug                     |   requestType = Bug               |    false               |
| Request                | Feature                 |   requestType = Feature Request   |    true                |
| Request                | Change Request          |   requestType = Change Request    |    false               |

**Behavior with Default Route Configured**
* When a source Request has requestType = Story (or any value not matching configured criteria), no explicit routing criteria is satisfied.
* In such cases, the *Default Route* is applied for the synchronization, For example, for requestType = Story, the target entity type will be Feature (as per the above configuration).

**Behavior When Default Route is Changed**

* Continuing the above scenario, a Request with requestType = Story is initially synchronized as a Feature.
* If the Default Route is changed to requestType = Bug route.
  * On the next synchronization, the existing target entity will be converted from Feature to Bug.

**Behavior When Default Route is Disabled**

* If the Default Route is disabled and an entity does not match any routing criteria:
  * The synchronization will fail with the error message: "OpsHub-020604: No routing criteria matched the provided entity values. Review the currently configured routing criteria: {currently configured criteria}"

<code class="expression">space.vars.SITENAME</code> allows seamless conversion when the routing field value changes and automatically updates the corresponding target entity type. It also ensures that when updates flow in the reverse direction, the source field value is adjusted accordingly—maintaining complete bidirectional consistency. For more details about configuration, refer to this section: [Routing Rules Configuration](integration-configuration.md#rule-based-routing).
