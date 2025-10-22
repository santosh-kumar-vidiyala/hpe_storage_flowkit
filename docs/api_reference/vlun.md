---
title: VLUNWorkflow
---

# VLUNWorkflow

Export / unexport volumes and volume sets to hosts and host sets (Virtual LUN mappings). Supports optional manual LUN assignment and port targeting.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `export_volume_to_host()` | Export volume to a host. |
| `unexport_volume_from_host()` | Remove host export. |
| `export_volume_to_hostset()` | Export volume to host set. |
| `unexport_volume_from_hostset()` | Remove host set export. |
| `export_volumeset_to_host()` | Export volume set to host. |
| `unexport_volumeset_from_host()` | Remove export of set from host. |
| `export_volumeset_to_hostset()` | Export volume set to host set. |
| `unexport_volumeset_from_hostset()` | Remove set export from host set. |

**Common Parameters**
| Name | Type | Description |
|------|------|-------------|
| volume_name / volume_set_name | str | Volume or volume set being exported. |
| host_name / host_set_name | str | Target host or host set. |
| lun | int | Explicit LUN number (omit if `autolun=True`). |
| node_val, slot, card_port | int | Port addressing components (implementation maps to physical port). |
| autolun | bool | If True, array assigns next available LUN. |

**Preprocessing:** `build_payload` assembles export payload, `find_vlun` checks for existing mappings for idempotence, validates host/volume existence and ensures no duplicate LUN conflict.

**Returns:** dict - Mapping result (or indication of existing mapping for idempotence). Unexport operations return confirmation or no-op.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.