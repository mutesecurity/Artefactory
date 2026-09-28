# DEFAULT Registry Hive
Aliases: DEFAULT, HKEY_USERS\.DEFAULT, system default settings
Category: Windows / Registry Hives

## What it is
The machine's `DEFAULT` hive, mounted as `HKEY_USERS\.DEFAULT` in a live registry. Its name is easy to confuse with the template profile used when creating new user profiles.

## Artefact location
- Hive: `%SystemRoot%\System32\config\DEFAULT` (normally `C:\Windows\System32\config\DEFAULT`).
- Collect same-directory `DEFAULT.LOG1` and `DEFAULT.LOG2` when present.
- The separate new-user template hive is normally `C:\Users\Default\NTUSER.DAT`; acquire it separately if the provisioning baseline is relevant.

## Investigation prompts
- Do configuration values in this hive relate to the system context or pre-logon behaviour under examination?
- Is the question about the machine `DEFAULT` hive, an individual user's `NTUSER.DAT`, or the `C:\Users\Default` template?
- Are there relevant historical copies or transaction logs to compare with the main hive?

## Interpretation cautions
`HKEY_USERS\.DEFAULT` is not the currently signed-in user's `HKEY_CURRENT_USER`, and the `config\DEFAULT` file is not `C:\Users\Default\NTUSER.DAT`. Do not attribute a setting here to a specific human user without independent evidence. Registry key LastWrite values do not identify the actor or the particular value changed.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: Customize the default user profile](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/customize-the-default-user-profile-by-using-copyprofile)
