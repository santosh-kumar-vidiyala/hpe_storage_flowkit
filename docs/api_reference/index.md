---
title: API Reference
---

# API Reference

This section provides reference documentation for each workflow class in the HPE Storage FlowKit. Workflows encapsulate domain logic, REST/SSH interactions, idempotent checks, and preprocessing helpers that sanitize user inputs before they are sent to the array.

**Workflow Index**

| Workflow | Purpose | Link |
|----------|---------|------|
| CPG | Manage Common Provisioning Groups (create/delete). | [Open](cpg.md) |
| Volume | Create, modify, grow, tune, delete volumes. | [Open](volume.md) |
| Snapshot | Snapshot lifecycle: create, promote, delete. | [Open](snapshot.md) |
| Clone | Physical copy orchestration (online/offline copy). | [Open](clone.md) |
| VLUN | Export/unexport volumes & sets to hosts/host sets. | [Open](vlun.md) |
| Host | Host lifecycle & initiator / CHAP management. | [Open](host.md) |
| Host Set | Group hosts; manage membership. | [Open](hostset.md) |
| Volume Set | Group volumes; manage membership & export. | [Open](volumeset.md) |
| QoS | QoS policy CRUD and listing. | [Open](qos.md) |
| Remote Copy Group | Remote replication groups & volumes control. | [Open](remote_copy_group.md) |
| System | System level status & metadata retrieval. | [Open](system.md) |

**Preprocessing Helpers Overview**

Many methods call a preprocessing function (e.g. `preprocess_create_volume`) before performing the REST/SSH action. Purposes include:

* Normalizing parameter names and units (e.g. converting size + unit to MiB).
* Building action payloads (e.g. setting action IDs for grow/tune operations).
* Validating user input and raising early Python exceptions rather than returning array errors.
* Idempotence: skipping operations when objects already exist or parameters imply no change.

Detailed notes for each method appear on its workflow page under the "Preprocessing" subsection.

**Using Workflows via AnsibleClient**

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