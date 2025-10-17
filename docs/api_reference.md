---
title: API Reference
---

# API Reference

This section provides reference documentation for each workflow class in the HPE Storage FlowKit. Workflows encapsulate domain logic, REST/SSH interactions, idempotent checks, and preprocessing helpers that sanitize user inputs before they are sent to the array.

## Workflow Index

| Workflow | Purpose | Link |
|----------|---------|------|
| CPGWorkflow | Manage Common Provisioning Groups (create/delete). | [Open](api/cpg.md) |
| VolumeWorkflow | Create, modify, grow, tune, delete volumes. | [Open](api/volume.md) |
| SnapshotWorkflow | Snapshot lifecycle: create, promote, delete. | [Open](api/snapshot.md) |
| CloneWorkflow | Physical copy orchestration (online/offline copy). | [Open](api/clone.md) |
| VLUNWorkflow | Export/unexport volumes & sets to hosts/host sets. | [Open](api/vlun.md) |
| HostWorkflow | Host lifecycle & initiator / CHAP management. | [Open](api/host.md) |
| HostSetWorkflow | Group hosts; manage membership. | [Open](api/hostset.md) |
| VolumeSetWorkflow | Group volumes; manage membership & export. | [Open](api/volumeset.md) |
| QOSWorkflow | QoS policy CRUD and listing. | [Open](api/qos.md) |
| RemoteCopyGroupWorkflow | Remote replication groups & volumes control. | [Open](api/remote_copy_group.md) |
| SystemWorkflow | System level status & metadata retrieval. | [Open](api/system.md) |

## Preprocessing Helpers Overview

Many methods call a preprocessing function (e.g. `preprocess_create_volume`) before performing the REST/SSH action. Purposes include:

* Normalizing parameter names and units (e.g. converting size + unit to MiB).
* Building action payloads (e.g. setting action IDs for grow/tune operations).
* Validating user input and raising early Python exceptions rather than returning array errors.
* Idempotence: skipping operations when objects already exist or parameters imply no change.

Detailed notes for each method appear on its workflow page under the "Preprocessing" subsection.

## Using Workflows via AnsibleClient

```python
from hpe_storage_flowkit.src.ansible_client import AnsibleClient

client = AnsibleClient(api_url="https://array.example", username="admin", password="secret")
client.create_volume(
    name="demo-vol",
    cpg="FC_r5",
    size=10,
    size_unit="GiB",
    params={"compression": True}
)
```

The `AnsibleClient` inherits all workflow methods; each exposes a high-level operation with built-in preprocessing and idempotent checks.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.