---
title: HPE Storage Flowkit
---

# HPE Storage Flowkit

Workflow‑centric Python toolkit for HPE Storage arrays. It layers orchestration and idempotent behaviors over raw REST endpoints, providing high‑level workflow classes you can call directly or via the composite `AnsibleClient`.

## Key Concepts

| Concept | Description |
|---------|-------------|
| Workflow Classes | Domain‑specific facades (VolumeWorkflow, SnapshotWorkflow, etc.) mapping method calls to REST endpoints or SSH commands. |
| Idempotence | Methods aim to avoid unnecessary changes; existence checks precede destructive operations. |
| Composite Client | `AnsibleClient` aggregates all workflows into a single interface for automation. |

## Quick Start

```python
from hpe_storage_flowkit.src.session import SessionManager
from hpe_storage_flowkit.src.workflows.volume import VolumeWorkflow

sm = SessionManager("https://array.example", username="admin", password="secret")
volumes = VolumeWorkflow(sm)
volumes.create_volume("demo_vol", {"cpg": "FC_r5", "sizeMiB": 10240})
```

## API Reference

Access full method signatures, parameters, return types, and REST mappings:

- **[API Reference](api_reference.html)** lists all workflows.

## Workflows At A Glance

| Workflow | Purpose | Link |
|----------|---------|------|
| CPGWorkflow | Manage Common Provisioning Groups. | [Open](api/cpg.html) |
| VolumeWorkflow | CRUD, growth, tuning of volumes. | [Open](api/volume.html) |
| SnapshotWorkflow | Create / promote / delete snapshots. | [Open](api/snapshot.html) |
| CloneWorkflow | Physical copy operations. | [Open](api/clone.html) |
| VLUNWorkflow | Export volumes/sets to hosts/host sets. | [Open](api/vlun.html) |
| HostWorkflow | Host lifecycle & initiator management. | [Open](api/host.html) |
| HostSetWorkflow | Group hosts for shared operations. | [Open](api/hostset.html) |
| VolumeSetWorkflow | Group volumes for policy/export. | [Open](api/volumeset.html) |
| QOSWorkflow | Define and manage QoS policies. | [Open](api/qos.html) |
| RemoteCopyGroupWorkflow | Remote replication group control. | [Open](api/remote_copy_group.html) |
| SystemWorkflow | System metadata retrieval. | [Open](api/system.html) |

## Next Steps

1. Explore a workflow page (e.g., VolumeWorkflow) to see endpoints and parameter tables.
2. Integrate with automation by composing workflows inside your toolchain.
3. Add CI to rebuild this site using `mkdocs build` on commits.

## Contributing

Pull requests: ensure new methods have updated docs. Automated generation script (future) will live under `tools/`. Proposals welcome.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.
