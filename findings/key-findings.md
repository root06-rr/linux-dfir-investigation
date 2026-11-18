# Key Forensic Findings

1. **Initial Access via Spear-Phishing (`email_invoice.eml` & `invoice_Q1_2075.ods`):**
   * User `j.morgan@robbco.com` received a targeted invoice lure from `akeane@poseidonenergy.net`. Opening `invoice_Q1_2075.ods` executed embedded shell commands that dumped local user accounts, session data, and `.bash_history` to `/tmp/invoice_dump.txt` and targeted `http://192.168.0.100:8080/collect.php`.
2. **Multi-Stage Command & Control Infrastructure:**
   * **Unprivileged Shell (`/tmp/.syncd` -> `/tmp/.x`):** Established an interactive Bash reverse shell to `10.0.0.66:4444` under `j.morgan`.
   * **Elevated Shell (`/usr/local/bin/sysmon`):** Established a second interactive Bash reverse shell to `10.0.0.66:5555` under administrative privileges.
3. **Privilege Escalation via `sudo` Misconfiguration:**
   * Rather than using a software exploit, the attacker leveraged `j.morgan`'s existing `sudo` rights to edit `/home/r.house/.ssh/authorized_keys` with `nano`, injecting an unauthorized public key and authenticating as `r.house` at `03:15:00`.
4. **Persistence Masquerading & Deception:**
   * The backdoor `/usr/local/bin/sysmon` was named to mimic a legitimate system monitoring tool and paired with a fabricated log file (`/opt/robbco/sys/boot_monitor.log` referencing `bios_hook: UOS boot intercepted at 0x400f2`).
5. **Source-Code Staging & Attempted Exfiltration:**
   * Proprietary bootloader and firmware code (`/opt/robbco/engineering/MFBootAgent/mfboot_main.c`, referencing `RETROS-52EE5` and `UOS-2.3.0`) was compressed, Base64-encoded, and staged in shared memory at `/dev/shm/.core_dump_2025.tgz.enc`.
