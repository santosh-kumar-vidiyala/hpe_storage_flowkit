---
title: CloneWorkflow
---

# CloneWorkflow

Physical copy (clone) orchestration: create, monitor, stop/resync copies.

**Methods Overview**
| Method | Purpose |
|--------|---------|
| `onlinePhysicalCopyExists()` | Check online physical copy existence & task state. |
| `offlinePhysicalCopyExists()` | Check offline copy existence. |
| `copyVolume()` | Initiate physical copy. |
| `stopOfflinePhysicalCopy()` | Stop an offline copy task. |
| `resyncPhysicalCopy()` | Resync an existing physical copy pair. |

**copyVolume**
Signature: `copyVolume(src_name, dest_name, dest_cpg, optional=None)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| src_name | str | Yes | Source volume. |
| dest_name | str | Yes | Destination (new) volume name. |
| dest_cpg | str | Yes | CPG for destination volume. |
| optional | dict | No | Tuning / priority / snapshot options. |

**Preprocessing:** `preprocess_copyVolume` ensures source exists, destination absent, normalizes optional flags, creates action payload.

**Returns:** dict - Copy task metadata.

**resyncPhysicalCopy**
Signature: `resyncPhysicalCopy(volume_name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| volume_name | str | Yes | Name of physical copy volume to resync. |

**Preprocessing:** Sets `action: RESYNC_PHYSICAL_COPY` constant; validates pair state.

**Returns:** dict - Resync task response.

**stopOfflinePhysicalCopy**
Signature: `stopOfflinePhysicalCopy(name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Copy volume name. |

**Preprocessing:** Builds payload with `action: STOP_PHYSICAL_COPY`; ensures copy in progress.

**Returns:** dict - Stop operation response.

Other existence check methods return boolean plus task info (implementation specifics omitted here).

---
© 2025 Hewlett Packard Enterprise. All rights reserved.