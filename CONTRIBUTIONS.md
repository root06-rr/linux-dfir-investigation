# Project Scope and Contributions

## My work

I completed this Linux DFIR investigation in an isolated TryHackMe lab and documented the investigation from my point of view. I reviewed the triage output, examined the listed Linux artifacts, compared the captured reconnaissance history with the local shell history, inspected suspicious scripts and source-code files, and decoded the staged archive.

This repository organizes that work into ten investigation stages, a command reference, an evidence index, a reconstructed timeline, key findings, security recommendations, and investigation limitations.

## Source boundaries

The project is based on the original Notion investigation and the existing screenshots and documentation in this repository.

- The lab-provided `classify_logs.py` and `file_anomalies.py` scripts are referenced but their source code is not included.
- The ten screenshots are retained from the original investigation.
- No new attack steps, scripts, datasets, execution results, packet captures, or network-transfer claims have been added.
- Interpretations are limited to the artifacts described in the investigation. Where execution, automatic persistence, SSH key contents, or successful external transfer are not independently demonstrated, the documentation says so.

## Original investigation record

[Digital Forensics Incident Report: Intrusion Analysis & Source Code Exfiltration](https://app.notion.com/p/3e4f055fceba80cc9278e36490d039f2)
