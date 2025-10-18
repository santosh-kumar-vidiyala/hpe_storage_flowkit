---
title: RemoteCopyGroupWorkflow
---

# RemoteCopyGroupWorkflow

Orchestrate remote replication groups, volume admissions, synchronization, and target/links management.

**Methods Overview (Selected)**

| Method | Purpose |
|--------|---------|
| `create_remote_copy_group()` | Create group. |
| `delete_remote_copy_group()` | Delete group. |
| `modify_remote_copy_group()` | Adjust local settings & targets. |
| `remote_copy_group_status()` | Fetch status. |
| `add_volume_to_remote_copy_group()` | Admit volume. |
| `remove_volume_from_remote_copy_group()` | Remove volume. |
| `start_remote_copy_group()` | Start replication. |
| `stop_remote_copy_group()` | Stop replication. |
| `synchronize_remote_copy_group()` | Force synchronization. |
| `admit_remote_copy_links()` | Establish links. |
| `dismiss_remote_copy_links()` | Remove links. |
| `admit_remote_copy_target()` | Add target. |
| `dismiss_remote_copy_target()` | Remove target. |
| `show_remote_copy_service()` | Display service info. |
| `rcopy_link_exists()` | Check link existence. |
| `start_remote_copy_service()` | Start replication service. |

**create_remote_copy_group**
Signature: `create_remote_copy_group(remote_copy_group_name, domain, remote_copy_targets, local_user_cpg, local_snap_cpg)`

| Parameter | Type | Description |
|-----------|------|-------------|
| remote_copy_group_name | str | Group name. |
| domain | str | Optional domain. |
| remote_copy_targets | list[dict] | Target definitions (name, mode, etc.). |
| local_user_cpg | str | Local user CPG. |
| local_snap_cpg | str | Local snapshot CPG. |

**Preprocessing:** Validates target structures, ensures group non-existence, checks CPG availability.

**Returns:** dict - Group resource.

Other methods perform similar validation (volume existence, target availability, link uniqueness) before executing REST/SSH commands.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.