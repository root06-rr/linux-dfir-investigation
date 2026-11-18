# Security & Hardening Recommendations

1. **Enforce Least Privilege on `sudo` Policies:**
   * Restrict `j.morgan` and non-administrative users from executing interactive editors (`nano`, `vi`, `vim`) as `root` or modifying files inside other users' `~/.ssh/` directories. Replace broad `sudo` rules with tightly scoped command allowlists.
2. **Harden Temporary and Shared-Memory Mounts (`/tmp` & `/dev/shm`):**
   * Mount `/tmp` and `/dev/shm` with `noexec`, `nosuid`, and `nodev` options in `/etc/fstab` to prevent direct execution of staged payloads such as `/tmp/.x`.
3. **Deploy File Integrity Monitoring (FIM) & Binary Path Controls:**
   * Monitor `/usr/local/bin`, `/etc/ssh`, and `/home/*/.ssh/authorized_keys` for unauthorized file creation or modification, which would immediately flag `/usr/local/bin/sysmon` and SSH key injection.
4. **Restrict Document Macro & External Command Execution:**
   * Enforce endpoint policies and mail-gateway scanning to block or sandbox `.ods` and `.odt` attachments capable of invoking external shell commands.
5. **Restrict Egress Network Traffic:**
   * Apply outbound firewall rules blocking unauthorized workstation connections to arbitrary external ports (`4444`, `5555`, `8080`).
