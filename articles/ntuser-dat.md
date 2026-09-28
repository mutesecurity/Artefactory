# NTUSER.DAT
Aliases: NTUSER, user registry hive, HKCU, HKEY_USERS SID
Category: Windows / Registry Hives

## What it is
The per-user registry hive loaded when a profile is used. For the signed-in user, its settings appear through `HKEY_CURRENT_USER`; a loaded profile can also appear beneath `HKEY_USERS\<SID>`.

## Artefact location
- Hive: `%SystemDrive%\Users\<profile>\NTUSER.DAT` (normally `C:\Users\<profile>\NTUSER.DAT`). The actual profile path may differ; check `SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList\<SID>\ProfileImagePath`.
- Collect adjacent `NTUSER.DAT.LOG1` and `NTUSER.DAT.LOG2` when present. Capture each relevant user's profile, including service profiles where in scope.
- Separate per-user classes hive: `%LOCALAPPDATA%\Microsoft\Windows\UsrClass.dat` (normally within that profile's `AppData\Local`); it is not part of `NTUSER.DAT`.

## Investigation prompts
- `Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`: do parsed entries suggest shell-mediated program or shortcut activity?
- `Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` and `...\RunMRU`: what recent-item or Run-dialog traces are present?
- `Software\Microsoft\Windows\CurrentVersion\Run` and `RunOnce`: which per-user logon launch entries are configured?
- Which SID and profile path does this hive belong to? Compare results with event logs, LNK files, Jump Lists, and application records.

## Interpretation cautions
`HKCU` is a view of the current process user's settings, not a single universal file. Entries are not a complete activity log; their presence, absence, order, and LastWrite times need artefact-specific interpretation. UserAssist is scoped to particular shell interactions, not every process launch. Avoid equating a profile-folder name with a verified identity. Preserve transaction logs when acquiring a live profile.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: About User Profiles](https://learn.microsoft.com/en-us/windows/win32/shell/about-user-profiles)
- [Magnet Forensics: UserAssist forensic artefacts](https://www.magnetforensics.com/blog/artifact-profile-userassist/)
