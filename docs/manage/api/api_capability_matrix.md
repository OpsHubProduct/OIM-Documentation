# API Capability Matrix - <code class="expression">space.vars.SITENAME</code>

This document provides an overview of API capabilities available in <code class="expression">space.vars.SITENAME</code>.  
It outlines which operations (Get, Create, Update, Delete, List, Execute) are supported for each feature across Integration and Admin modules.  
Use this matrix as a quick reference to understand API coverage and identify gaps.

---

## Legend

| Symbol | Meaning            |
|--------|--------------------|
| ✅     | Available in API   |
| ❌     | Missing in API     |
| —      | Not Applicable     |

---

## Integration

| Feature / Module      | Get | Create | Update | Delete | List | Execute | Notes                                                                 |
|----------------------|-----|--------|--------|--------|------|---------|-----------------------------------------------------------------------|
| Excel Upload         | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| Workflow             | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| System               | ✅  | ✅     | ✅     | —      | ✅   | —       | —                                                                     |
| System Type          | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| System Template      | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| Mapping              | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| Integration          | ✅  | ✅     | ✅     | ✅     | ✅   | ✅      | <span style="color:red;">API to get sync log files</span>              |
| Reconcile            | ✅  | —      | —      | —      | —    | ✅      | —                                                                     |
| Failure Notification | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| Folder               | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                                                                     |
| Global Failure       | ✅  | —      | —      | ✅     | ✅   | —       | —                                                                     |
| Processing Failure   | ✅  | —      | ✅     | ✅     | ✅   | ✅      | —                                                                     |
| Sync Report          | —   | —      | —      | —      | ❌   | —       | —                                                                     |
| Audits               | —   | —      | —      | —      | ❌   | —       | —                                                                     |

---

## Admin

| Feature / Module   | Get | Create | Update | Delete | List | Execute | Notes               |
|-------------------|-----|--------|--------|--------|------|---------|---------------------|
| System Information| ❌  | —      | —      | —      | —    | —       | —                   |
| User              | ❌  | ❌     | ❌     | —      | ✅   | —       | —                   |
| User-Role         | ✅  | —      | ✅     | —      | —    | —       | —                   |
| Role              | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                   |
| Usage Report      | ✅  | —      | —      | —      | —    | —       | —                   |
| Log Setting       | ✅  | —      | ✅     | —      | —    | —       | —                   |
| SDK               | ✅  | ✅     | ✅     | —      | ✅   | —       | —                   |
| Scheduler         | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                   |
| Trends Dashboard  | —   | —      | —      | —      | —    | —       | —                   |
| Login Server Mgmt | ❌  | ❌     | ❌     | ❌     | ❌   | ❌      | —                   |
| License           | —   | —      | —      | —      | —    | —       | Not there by design |
| Purge             | —   | —      | —      | —      | —    | —       | Not there by design |
| Rules             | —   | —      | —      | —      | —    | —       | Not there by design |