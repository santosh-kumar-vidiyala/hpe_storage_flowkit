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

Access full method signatures, parameters, return types, and REST/SSH mappings:

- **[API Reference](api_reference.md)** lists all workflows and preprocessing notes.

## Workflows At A Glance

| Workflow | Purpose | Link |
|----------|---------|------|
| CPGWorkflow | Manage Common Provisioning Groups. | [Open](api/cpg.md) |
| VolumeWorkflow | CRUD, growth, tuning of volumes. | [Open](api/volume.md) |
| SnapshotWorkflow | Create / promote / delete snapshots. | [Open](api/snapshot.md) |
| CloneWorkflow | Physical copy operations. | [Open](api/clone.md) |
| VLUNWorkflow | Export volumes/sets to hosts/host sets. | [Open](api/vlun.md) |
| HostWorkflow | Host lifecycle & initiator management. | [Open](api/host.md) |
| HostSetWorkflow | Group hosts for shared operations. | [Open](api/hostset.md) |
| VolumeSetWorkflow | Group volumes for policy/export. | [Open](api/volumeset.md) |
| QOSWorkflow | Define and manage QoS policies. | [Open](api/qos.md) |
| RemoteCopyGroupWorkflow | Remote replication group control. | [Open](api/remote_copy_group.md) |
| SystemWorkflow | System metadata retrieval. | [Open](api/system.md) |
| Schedule Operations | Snapshot schedule lifecycle (create/modify/suspend/resume). | [Open](api/schedule.md) |

## Next Steps

1. Explore a workflow page (e.g., VolumeWorkflow) to see endpoints and parameter tables.
2. Integrate with automation by composing workflows inside your toolchain.
3. Add CI to rebuild this site using `mkdocs build` on commits.

## Contributing

Pull requests: ensure new methods have updated docs. Automated generation script (future) will live under `tools/`. Proposals welcome.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.
