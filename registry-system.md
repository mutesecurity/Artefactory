# SYSTEM Registry Hive
Aliases: SYSTEM, HKLM\SYSTEM, control sets, services, device enumeration
Category: Windows / Registry Hives

## What it is
The machine hive for startup configuration, services, drivers, and device configuration. In a live registry it appears as `HKEY_LOCAL_MACHINE\SYSTEM`.

## Artefact location
- Hive: `%SystemRoot%\System32\config\SYSTEM` (normally `C:\Windows\System32\config\SYSTEM`).
- Collect same-directory `SYSTEM.LOG1` and `SYSTEM.LOG2` when present. Keep any other associated supporting files with the original acquisition.
- An offline hive contains `ControlSet00x` keys. Read `SYSTEM\Select` to determine which control set was current at acquisition; inspect other control sets where relevant. `CurrentControlSet` is the convenient live-registry view.

## Investigation prompts
- `ControlSet00x\Services`: which services or drivers were configured, and what are their image paths, start types, and accounts?
- `ControlSet00x\Enum`: which device instances and hardware identifiers were registered? Correlate with `setupapi.dev.log` and device-related event logs.
- `ControlSet00x\Control`: which startup and device configuration settings matter to the question?

## Interpretation cautions
An enumerated device or configured service does not alone prove a particular use or execution time. A key's LastWrite time marks an update to that key, not necessarily creation of a specific value. Do not interpret `CurrentControlSet` as a separate file or assume `ControlSet001` was always current. Preserve and consider transaction logs when parsing a live-acquired hive.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: HKLM SYSTEM Services registry tree](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree)
- [Microsoft: HKLM SYSTEM Enum registry tree](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/hklm-system-currentcontrolset-enum-registry-tree)
