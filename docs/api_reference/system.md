---
title: SystemWorkflow
---

# SystemWorkflow

Retrieve high-level system metadata, status, capacity and configuration details.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `get_system_status()` | Returns health/status summary. |
| `get_capacity()` | Fetch capacity utilization metrics. |
| `list_ports()` | Enumerate system ports and their state. |

> Actual method names reflect those implemented in `SystemWorkflow`; adapt above if naming differs.

**Preprocessing:** Minimal; primarily wraps REST GET calls with exception translation and may collate multiple endpoint results for convenience.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.