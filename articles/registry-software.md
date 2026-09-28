# SOFTWARE Registry Hive
Aliases: SOFTWARE, HKLM\SOFTWARE, installed software, ProfileList
Category: Windows / Registry Hives

## What it is
The machine hive for operating-system and application configuration. In a live registry it appears as `HKEY_LOCAL_MACHINE\SOFTWARE`.

## Artefact location
- Hive: `%SystemRoot%\System32\config\SOFTWARE` (normally `C:\Windows\System32\config\SOFTWARE`).
- Collect same-directory `SOFTWARE.LOG1` and `SOFTWARE.LOG2` when present.

## Investigation prompts
- `Microsoft\Windows NT\CurrentVersion`: what OS build and installation details are recorded? Compare with other sources for the examined build.
- `Microsoft\Windows NT\CurrentVersion\ProfileList\<SID>`: which profile path is associated with a SID?
- `Microsoft\Windows\CurrentVersion\Uninstall` and `WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall`: what machine-wide uninstall entries exist? Also examine each user's uninstall keys in their profile hive.
- `Microsoft\Windows\CurrentVersion\Run` and `RunOnce`: which machine-wide logon launch entries are configured?

## Interpretation cautions
An uninstall entry does not prove an application is still installed or was executed. Portable and per-user software may have no machine-wide entry. A `ProfileList` mapping does not by itself establish that a named user logged on during the period of interest. Registry views and 32-bit redirection can affect which path a tool displays. Preserve transaction logs and corroborate with files, event logs, and user hives.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: Windows registry information for advanced users](https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/windows-registry-advanced-users)
- [Microsoft: Run and RunOnce registry keys](https://learn.microsoft.com/en-us/windows/win32/setupapi/run-and-runonce-registry-keys)
