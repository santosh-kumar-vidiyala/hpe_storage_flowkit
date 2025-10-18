---
title: Schedule Operations
---

# Schedule Operations

Snapshot schedule lifecycle utilities exposed directly on `AnsibleClient` (not a separate workflow class). These methods manage recurring snapshot tasks with retention and expiration policies.

**Methods Overview**

| Method | Purpose |
|--------|---------|
| `scheduleExists()` | Check if schedule exists. |
| `createSchedule()` | Create a new snapshot schedule. |
| `deleteSchedule()` | Delete an existing schedule. |
| `modifySchedule()` | Modify schedule name and/or frequency. |
| `getSchedule()` | Retrieve schedule definition. |
| `getScheduleStatus()` | Retrieve current status/state. |
| `suspendSchedule()` | Suspend execution of schedule. |
| `resumeSchedule()` | Resume a suspended schedule. |

**Common Payload Keys (createSchedule)**
| Key | Type | Description |
|-----|------|-------------|
| read_only | bool | If True, snapshots created read-only. |
| expiration_time | int | Time value before expiration. |
| expiration_unit | str | Unit for expiration (e.g. `hours`, `days`). Converted internally to hours. |
| retention_time | int | Time to retain before deletion. |
| retention_unit | str | Unit for retention (e.g. `hours`, `days`). Converted internally to hours. |
| base_volume_name | str | Source volume for scheduled snapshots. |

**Preprocessing:** `preprocess_create_schedule(expiration_time, retention_time, expiration_unit, retention_unit)` converts units to hours and validates non-zero durations. If either duration resolves to 0 hours, creation aborts with an error (idempotent safeguard).

**createSchedule**
Signature: `createSchedule(schedule_name, taskfreq, payload)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| schedule_name | str | Yes | Unique schedule name. |
| taskfreq | str | Yes | Frequency string (e.g. `hourly`, `daily`, cron-like tokens) consumed by underlying CLI/SSH. |
| payload | dict | Yes | See payload keys above. |

**Returns:** tuple `(changed, failed, message, data)` reflecting creation result.

**modifySchedule**
Signature: `modifySchedule(name, new_name, task_freq)`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | str | Yes | Existing schedule name. |
| new_name | str | No | New name to rename schedule. |
| task_freq | str | No | Updated frequency string. |

**Preprocessing:** Builds `setsched` command options only for changed values; skips no-op modifications.

**suspendSchedule / resumeSchedule**
Both validate existence (`scheduleExists`) before invoking underlying SSH command. Return tuple `(changed, failed, message, data)`; if absent, return `(False, False, "Schedule does not exist", {})`.

**deleteSchedule**
Validates existence and issues force removal command. Returns deletion task result or no-op tuple if schedule absent.

**Error Handling**
SSH command exceptions are caught and converted to message tuples; invalid preprocessing (zero retention/expiration) aborts early.

---
© 2025 Hewlett Packard Enterprise. All rights reserved.