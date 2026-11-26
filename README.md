Copyright (C) 2017 The LineageOS Project

Common device tree for Xiaomi MSM8998 based devices
=========================================

## Dragonite runtime policy

On products with `ax_dragonite.xml`, the following `Settings.Global` keys are
observed at runtime. Deleting a key restores its default. Settings changes
require the privileged settings writer (for example, `adb shell settings put global`).

| Key | Opt-in value | Effect |
| --- | --- | --- |
| `ax_dragonite_cpu_governor` | `performance` or `powersave` | Selects the CPU governor on each cluster. The default is `schedutil`. |
| `ax_dragonite_cpu_profile` | `performance` | Requests CPU frequency floors independently of transient scene votes. |
| `ax_dragonite_gpu_profile` | `performance` | Requests a 342 MHz GPU floor independently of transient rendering votes. |
| `ax_dragonite_thread_policy` | `fair` | Heavy UI leases can raise the main and render threads' fair priority without changing their scheduler class or moving them between cpusets. This replaces the optional realtime promotion while selected. |
| `ax_dragonite_memory_profile` | `retain-activities` | Compact only empty cached processes at freeze time. Does not change LMKD, freezer eligibility, or mmd. |

The Power HAL owns the node writes and restores defaults when a mode ends.
Frequency floors are requests, not replacements for frequency ceilings or
thermal limits. Turning off `ax_dragonite_enabled` releases the runtime modes
and scene leases without deleting settings.
