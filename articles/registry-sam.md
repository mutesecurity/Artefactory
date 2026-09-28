# SAM Registry Hive
Aliases: SAM, Security Accounts Manager, HKLM\SAM, local accounts
Category: Windows / Registry Hives

## What it is
The Security Accounts Manager stores local account and group information. Its registry hive is exposed as `HKEY_LOCAL_MACHINE\SAM` in the live registry, subject to access controls.

## Artefact location
- Hive: `%SystemRoot%\System32\config\SAM` (normally `C:\Windows\System32\config\SAM`).
- Collect same-directory `SAM.LOG1` and `SAM.LOG2` when present.
- Preserve `SYSTEM` alongside it when an approved forensic workflow needs to interpret protected account material; handle both as sensitive evidence.

## Investigation prompts
- Which local users and groups are present, and what are their RIDs and account flags?
- Was a local account enabled or disabled? What corroborating account-management events are available?
- Do local account identifiers align with profile directories and `SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`?

## Interpretation cautions
The local SAM is not a complete directory of domain or cloud identities. Presence of an account does not prove a logon or activity by that person; use Security events and other independent records. Account metadata and parsed timestamps depend on the parser and Windows build. This hive can contain credential-derived material: restrict access and avoid putting extracted hashes or secrets in general case notes.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: Local accounts](https://learn.microsoft.com/en-us/windows/security/identity-protection/access-control/local-accounts)
- [Microsoft: Credentials processes in Windows authentication](https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication)
