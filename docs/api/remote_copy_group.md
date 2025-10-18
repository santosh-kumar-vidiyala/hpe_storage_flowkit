---
title: RemoteCopyGroupWorkflow
---

# RemoteCopyGroupWorkflow

Orchestrate remote replication groups, volume admissions, synchronization, and target/links management.

**Methods Overview (Selected)**
| Method | Purpose |
|--------|---------|
| `create_remote_copy_group(remote_copy_group_name, domain, remote_copy_targets, local_user_cpg, local_snap_cpg)` | Create group. |
| `delete_remote_copy_group(remote_copy_group_name, keep_snap=False)` | Delete group. |
| `modify_remote_copy_group(remote_copy_group_name, local_user_cpg, local_snap_cpg, modify_targets, unset_user_cpg=False, unset_snap_cpg=False)` | Adjust local settings & targets. |
| `remote_copy_group_status(remote_copy_group_name)` | Fetch status. |
| `add_volume_to_remote_copy_group(remote_copy_group_name, volume_name, admit_volume_targets, snapshot_name=None, volume_auto_creation=False, skip_initial_sync=False, different_secondary_wwn=False)` | Admit volume. |
| `remove_volume_from_remote_copy_group(...)` | Remove volume. |
| `start_remote_copy_group(remote_copy_group_name, skip_initial_sync=False, target_name=None, starting_snapshots=None)` | Start replication. |
| `stop_remote_copy_group(remote_copy_group_name, no_snapshot=False, target_name=None)` | Stop replication. |
| `synchronize_remote_copy_group(remote_copy_group_name, no_resync_snapshot=False, target_name=None, full_sync=False)` | Force synchronization. |
| `admit_remote_copy_links(target_name, source_port, target_port_wwn_or_ip)` | Establish links. |
| `dismiss_remote_copy_links(target_name, source_port, target_port_wwn_or_ip)` | Remove links. |
| `admit_remote_copy_target(remote_copy_group_name, target_name, target_mode, local_remote_volume_pair_list=None)` | Add target. |
| `dismiss_remote_copy_target(remote_copy_group_name, target_name)` | Remove target. |
| `show_remote_copy_service()` | Display service info. |
| `rcopy_link_exists(target_name, source_port, target_port_wwn_or_ip)` | Check link existence. |
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