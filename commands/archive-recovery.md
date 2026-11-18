# Encoded Archive Recovery Workflow (Stage 10)

## Objective

Inspect the hidden file `/dev/shm/.core_dump_2025.tgz.enc`, decode its Base64 content, and extract the resulting archive into a separate directory under `/tmp` to identify the files it contains.

## Commands documented in the investigation

```bash
# 1. Inspect /dev/shm, including hidden files
cd /dev/shm
ls -la

# 2. Inspect the encoded file
cat .core_dump_2025.tgz.enc

# 3. Decode the Base64 content into a gzip-compressed tar archive
base64 -d /dev/shm/.core_dump_2025.tgz.enc > /tmp/stolen.tar.gz

# 4. Create an extraction directory and extract the archive
mkdir -p /tmp/stolen_source
tar -xzvf /tmp/stolen.tar.gz -C /tmp/stolen_source
```

## Recovered paths recorded in the investigation

- `opt/robbco/engineering/`
- `opt/robbco/engineering/MFBootAgent/`
- `opt/robbco/engineering/MFBootAgent/mfboot_main.c`

## What this establishes

The decode and extraction recovered the listed engineering source-code path from a locally staged archive in `/dev/shm`. This supports the finding that source code was packaged and staged on the host.

## What this does not establish

The recovered archive does not, by itself, prove that the data was transmitted outside the host. The investigation does not include packet captures or receiving-listener logs that confirm a successful external transfer.
