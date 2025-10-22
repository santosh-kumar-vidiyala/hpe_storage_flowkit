---
title: VolumeSetWorkflow
---

# VolumeSetWorkflow

Group volumes for policy management, exports and replication operations.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `create_volumeset()` | Create volume set. |
| `delete_volumeset()` | Delete volume set. |
| `add_volumes_to_volumeset()` | Add volumes. |
| `remove_volumes_from_volumeset()` | Remove volumes. |

**create_volumeset**
Signature: `create_volumeset(name, domain=None, setmembers=None)`

| Parameter | Type | Description |
|-----------|------|-------------|
| name | str | Volume set name. |
| domain | str | Optional domain. |
| setmembers | list[str] | Initial volume names. |

**Preprocessing:** Confirms each volume exists, filters duplicates, checks for existing set.

**Returns:** dict - Volume set resource.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.