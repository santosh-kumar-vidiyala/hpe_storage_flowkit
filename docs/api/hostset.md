---
title: HostSetWorkflow
---

# HostSetWorkflow

Group hosts for shared exports and policy application.

**Methods Overview**
| Method | Purpose |
|--------|---------|
| `create_hostset(name, domain=None, setmembers=None)` | Create host set. |
| `delete_hostset(name)` | Delete host set. |
| `add_hosts_to_hostset(name, setmembers)` | Add hosts. |
| `remove_hosts_from_hostset(name, setmembers)` | Remove hosts. |
| `get_hostset(name)` | Fetch host set details. |

**create_hostset**
Signature: `create_hostset(name, domain=None, setmembers=None)`

| Parameter | Type | Description |
|-----------|------|-------------|
| name | str | Host set name. |
| domain | str | Optional domain grouping. |
| setmembers | list[str] | Initial host member names. |

**Preprocessing:** Validates host existence for each member, filters duplicates, ensures host set not already present.

**Returns:** dict - Host set resource.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.