# SECURITY Registry Hive
Aliases: SECURITY, HKLM\SECURITY, LSA policy, cached domain logons
Category: Windows / Registry Hives

## What it is
A machine hive associated with Local Security Authority policy and protected authentication data. It is exposed as `HKEY_LOCAL_MACHINE\SECURITY` in a live registry; access is tightly controlled.

## Artefact location
- Hive: `%SystemRoot%\System32\config\SECURITY` (normally `C:\Windows\System32\config\SECURITY`).
- Collect same-directory `SECURITY.LOG1` and `SECURITY.LOG2` when present.
- Preserve `SYSTEM` with it when an authorised forensic workflow requires related protection material.

## Investigation prompts
- Do local security policy settings bear on the authentication or access-control question?
- Are cached domain logon records or LSA secret entries relevant to the case, and what independent logon evidence exists?
- Were the hive and its associated logs acquired consistently, without exposing secrets beyond the investigation team?

## Interpretation cautions
Cached credential material indicates a system capability or prior credential caching, not a complete sign-in timeline. Some data is protected and its interpretation depends on Windows version and security configuration. Handle this hive as sensitive evidence; do not export plaintext secrets or password-derived material into routine reports. Domain controllers and ordinary endpoints do not have identical account stores.

## Sources
- [Microsoft: Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Microsoft: Credentials processes in Windows authentication](https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication)
- [Microsoft: System key utility technical overview](https://learn.microsoft.com/en-us/windows-server/security/kerberos/system-key-utility-technical-overview)
