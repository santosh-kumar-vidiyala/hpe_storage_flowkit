---
title: HostWorkflow
---

# HostWorkflow

Manage host objects (initiator identities) and their attributes, CHAP security and path assignments.

**Methods Overview**
| Method | Purpose |
|--------|---------|
| `create_host(name, iscsiNames=None, FCWwns=None, host_domain=None, host_persona=None)` | Create host. |
| `delete_host(name)` | Delete host. |
| `modify_host(host_name, host_new_name, persona=None)` | Rename or change persona. |
| `add_initiator_chap(host_name, chap_name, chap_secret, chap_secret_hex=False)` | Configure initiator CHAP. |
| `remove_initiator_chap(host_name)` | Remove initiator CHAP. |
| `initiator_chap_exists(host_name)` | Check if initiator CHAP present. |
| `add_target_chap(host_name, chap_name, chap_secret, chap_secret_hex=False)` | Configure target CHAP. |
| `remove_target_chap(host_name)` | Remove target CHAP. |
| `queryHost(iqns=None, wwns=None)` | Query hosts by initiators. |
| `add_fc_path_to_host(host_name, host_fc_wwns)` | Add FC paths. |
| `remove_fc_path_from_host(host_name, host_fc_wwns, force_path_removal=False)` | Remove FC paths. |
| `add_iscsi_path_to_host(host_name, host_iscsi_names)` | Add iSCSI initiators. |
| `remove_iscsi_path_from_host(host_name, host_iscsi_names, force_path_removal=False)` | Remove iSCSI initiators. |

**create_host**
Signature: `create_host(name, iscsiNames=None, FCWwns=None, host_domain=None, host_persona=None)`

| Parameter | Type | Description |
|-----------|------|-------------|
| name | str | Host name. |
| iscsiNames | list[str] | iSCSI IQNs to associate. |
| FCWwns | list[str] | Fibre Channel WWNs. Normalized for formatting. |
| host_domain | str | Optional domain. |
| host_persona | int | Persona value (array-specific behavior profile). |

**Preprocessing:** Validates formatting of WWNs and IQNs, filters duplicates, ensures host does not exist.

**Returns:** dict - Host resource.

Other methods follow similar patterns: existence checks and normalization prior to REST/SSH calls. CHAP operations verify secrets length and hex encoding if requested.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.