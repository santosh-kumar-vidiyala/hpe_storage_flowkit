---
title: SnapshotWorkflow
---

# SnapshotWorkflow

Manage virtual copy snapshots: creation, deletion, and promotion (making a snapshot the active volume).

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `create_snapshot()` | Create snapshot of a base volume. |
| `delete_snapshot()` | Delete a snapshot. |
| `promoteVirtualCopy()` | Promote snapshot to base volume (restore). |

**create_snapshot**
Signature: `create_snapshot(volume_name, snapshot_name, optional=None)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| volume_name | str | Yes | Base volume name. |
| snapshot_name | str | Yes | New snapshot name. |
| optional | dict | No | Extra attributes (retention policy, read-only flag, etc.). |

**Preprocessing:** `preprocess_create_snapshot` validates that base volume exists, resolves optional flags, sets default retention or read-only, skips creation if snapshot already present.

**Returns:** dict - Snapshot resource.

**delete_snapshot**
Signature: `delete_snapshot(snapshot_name)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| snapshot_name | str | Yes | Snapshot name. |

**Preprocessing:** `preprocess_delete_snapshot` checks existence and dependency (promotion states) before deletion.

**Returns:** dict | None - Deletion result or None if snapshot absent.

**promoteVirtualCopy**
Signature: `promoteVirtualCopy(name, params)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Snapshot name to promote. |
| params | dict | Yes | Promotion options (e.g. priority, allowRSC). |

**Preprocessing:** `preprocess_promoteVirtualCopy` builds payload including action code, validates snapshot state and ensures not already promoted.

**Returns:** dict - Promotion task result.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.