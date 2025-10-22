---
title: VolumeWorkflow
---

# VolumeWorkflow

Operations for virtual volumes: create, inspect, modify, grow, tune and delete. Methods in `AnsibleClient` wrap underlying workflow logic and invoke preprocessing helpers to normalize inputs.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `create_volume()` | Create a new virtual volume. |
| `get_volume()` | Retrieve details for a volume. |
| `modify_volume()` | Update attributes (e.g. provisioning, userCPG). |
| `grow_volume()` | Increase capacity (operation + params determine growth). |
| `tune_volume()` | Adjust performance/provisioning characteristics. |
| `delete_volume()` | Delete a volume. |

**Method Reference**

**create_volume**
Signature: `create_volume(name, cpg, size, size_unit, params=None)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Name for the new volume. |
| cpg | str | Yes | User CPG providing storage. |
| size | int | Yes | Numeric size value before unit conversion. |
| size_unit | str | Yes | Unit string (MiB, GiB, TiB). Converted to MiB internally. |
| params | dict | No | Additional attributes (provisioning type, compression, dedup, snapCPG, etc.). |

**Preprocessing:** `preprocess_create_volume` validates size & unit, converts to MiB, applies defaults (e.g. provisioning type), filters unsupported keys and may raise if volume exists (idempotence).

**Returns:** dict - Created volume resource.

**get_volume**
Signature: `get_volume(name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Volume name. |

**Preprocessing:** None (direct REST retrieval). May wrap exceptions.

**Returns:** dict - Volume details.

**modify_volume**
Signature: `modify_volume(name, volume_mods, app_type=None)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Target volume name. |
| volume_mods | dict | Yes | Fields to change (e.g. newName, userCPG, provisioningType). |
| app_type | str | No | Optional application classification appended to payload if provided. |

**Preprocessing:** Internal validation of keys; may enrich payload with application metadata, removes no-op modifications.

**Returns:** dict - Updated resource state.

**grow_volume**
Signature: `grow_volume(name, operation, params)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Volume name. |
| operation | str | Yes | Growth mode keyword (e.g. `add`, `resize`). |
| params | dict | Yes | Operation-specific values (e.g. `additional_size`, `new_total_size`, unit). |

**Preprocessing:** `preprocess_grow_volume` reads current size (`get_volume`) and calculates new sizeMiB; returns 0 if no change, preventing unnecessary REST action.

**Returns:** dict - Growth operation result or idempotent no-op info.

**tune_volume**
Signature: `tune_volume(name, operation, params)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Volume name. |
| operation | str | Yes | Tuning action (e.g. `convert_provisioning`, `set_compression`). |
| params | dict | Yes | Required parameters for selected action. |

**Preprocessing:** `preprocess_tune_volume` inspects current volume details to build minimal delta (e.g. only change provisioning if different) and sets appropriate action codes.

**Returns:** dict - Tuning result or no-op indicator.

**delete_volume**
Signature: `delete_volume(name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Volume name to delete. |

**Preprocessing:** `preprocess_delete_volume` ensures volume exists and is safe to remove (e.g. not exported) before issuing REST delete. May raise early exception if constraints violated.

**Returns:** dict | None - Deletion response or None if already absent (idempotent).

**Examples**

```python
client.create_volume("db-vol", cpg="FC_r5", size=50, size_unit="GiB", params={"compression": True})
client.grow_volume("db-vol", operation="add", params={"additional": 10, "unit": "GiB"})
client.tune_volume("db-vol", operation="convert_provisioning", params={"newType": "tpvv"})
```

**Error Handling**
All methods may raise `HPEStorageException` (wrapped) for array-side errors; preprocessing raises `ValueError` or custom exceptions for invalid inputs prior to REST calls.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.