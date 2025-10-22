---
title: HPE Storage Flowkit
---

# HPE Storage Flowkit

Workflow‑centric Python toolkit for HPE Storage arrays. It layers orchestration and idempotent behaviors over raw REST endpoints, providing high‑level workflow classes you can call directly or via the composite `AnsibleClient`.

**Key Concepts**

| Concept | Description |
|---------|-------------|
| Workflow Classes | Domain‑specific facades (VolumeWorkflow, SnapshotWorkflow, etc.) mapping method calls to REST endpoints or SSH commands. |
| Idempotence | Methods aim to avoid unnecessary changes; existence checks precede destructive operations. |
| Composite Client | `AnsibleClient` aggregates all workflows into a single interface for automation. |

**Quick Start**

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

**Next Steps**

1. Explore a workflow page (e.g., VolumeWorkflow) to see endpoints and parameter tables.
2. Integrate with automation by composing workflows inside your toolchain.
3. Add CI to rebuild this site using `mkdocs build` on commits.

**Contributing**

Pull requests: ensure new methods have updated docs. Automated generation script (future) will live under `tools/`. Proposals welcome.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.
