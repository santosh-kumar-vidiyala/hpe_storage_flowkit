---
title: QOSWorkflow
---

# QOSWorkflow

Define and manage Quality of Service (QoS) policies restricting I/O (bandwidth, IOPS) on volumes or sets.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `create_qos()` | Create QoS rule. |
| `modify_qos()` | Modify QoS rule. |
| `delete_qos()` | Delete QoS rule. |
| `get_qos()` | Retrieve specific QoS. |
| `list_qos()` | List all QoS rules. |

**create_qos**
Signature: `create_qos(name, params)`

| Parameter | Type | Description |
|-----------|------|-------------|
| name | str | QoS rule name. |
| params | dict | Limits (maxIOPS, maxBandwidthMBps, scope members, priority). |

**Preprocessing:** `validate_qos_params` ensures numeric limits positive, mutually exclusive constraints handled, member scopes valid.

**Returns:** dict - QoS resource.

**modify_qos / delete_qos / get_qos / list_qos**
Standard CRUD patterns with validation of existence and parameter keys before REST calls.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.
