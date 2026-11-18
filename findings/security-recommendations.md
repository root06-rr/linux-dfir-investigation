# Security and Hardening Recommendations

These recommendations are based on the artifacts and attack paths described in the investigation. They are defensive recommendations, not controls that were implemented or tested as part of this lab.

## 1. Apply least privilege to sudo access

The captured shell history contains `sudo nano /home/r.house/.ssh/authorized_keys`. Review sudo rules and restrict interactive editors or other commands that allow users to modify another account's SSH configuration. Use narrowly scoped permissions rather than broad administrative access.

**Related evidence:** [Stage 07: Privilege escalation review](../investigation/07-privilege-escalation.md).

## 2. Monitor SSH authorized-keys files

Monitor changes to user SSH configuration and authorized-keys files. Review unexpected key additions and correlate file changes with authentication events.

**Related evidence:** [Stage 07: Privilege escalation review](../investigation/07-privilege-escalation.md).

## 3. Review temporary and shared-memory locations

The investigation found reconnaissance output and hidden scripts in `/tmp`, as well as a Base64-encoded archive in `/dev/shm`. Include these locations in file monitoring and incident-response review. Consider appropriate mount hardening, including `noexec`, `nosuid`, and `nodev`, after checking application compatibility and operational requirements.

**Related evidence:** [Stage 02: Temporary files](../investigation/02-temporary-files.md), [Stage 06: Reverse-shell analysis](../investigation/06-reverse-shell-analysis.md), and [Stage 10: Archive recovery](../investigation/10-archive-recovery.md).

## 4. Monitor executable paths and suspicious scripts

Review unexpected files in `/usr/local/bin` and monitor changes to system executable paths. Investigate files whose names resemble legitimate utilities but whose contents or provenance do not match expected software.

**Related evidence:** [Stage 08: Suspicious sysmon script](../investigation/08-ssh-persistence.md).

## 5. Restrict document-related command execution

Review controls for email attachments and office documents, including whether documents can invoke external commands or access sensitive local files. Use mail-gateway inspection and endpoint controls appropriate to the organization's environment.

**Related evidence:** [Stage 04: Attachment analysis](../investigation/04-phishing-analysis.md) and [Stage 05: Email investigation](../investigation/05-email-investigation.md).

## 6. Review outbound network activity

Investigate unexpected outbound connections to the IP addresses and ports recorded in the suspicious scripts and attachment contents: `10.0.0.66:4444`, `10.0.0.66:5555`, and `192.168.0.100:8080`. Use network telemetry to determine whether connections occurred. The lab artifacts in this repository do not independently establish successful connections.

**Related evidence:** [Stage 04: Attachment analysis](../investigation/04-phishing-analysis.md), [Stage 06: Reverse-shell analysis](../investigation/06-reverse-shell-analysis.md), and [Stage 08: Suspicious sysmon script](../investigation/08-ssh-persistence.md).
