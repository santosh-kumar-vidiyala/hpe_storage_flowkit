---
title: CPGWorkflow
---

# CPGWorkflow

Manage Common Provisioning Groups (CPGs) which define underlying storage pool characteristics.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `create_cpg()` | Create a new CPG. |
| `delete_cpg()` | Delete an existing CPG. |

**create_cpg**
Signature: `create_cpg(name, params)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | CPG name. |
| params | dict | No | Characteristics (e.g. growth increment, RAID type) as supported. |

**Preprocessing:** `preprocess_create_cpg` validates RAID type, growth parameters, filters unsupported keys, ensures non-existence for idempotence.

**Returns:** dict - Created CPG.

**delete_cpg**
Signature: `delete_cpg(name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | CPG name. |

**Preprocessing:** `preprocess_delete_cpg` confirms existence, checks dependent volumes count to avoid deleting in-use pools.

**Returns:** dict | None - Deletion response or None if absent.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.