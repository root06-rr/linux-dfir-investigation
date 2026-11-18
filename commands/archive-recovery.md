# Encoded Archive Recovery Workflow (Stage 10)

## Objective
Safely inspect, Base64-decode, and extract the hidden staged payload `/dev/shm/.core_dump_2025.tgz.enc` into an isolated directory under `/tmp` to verify its contents.

## Step-by-Step Commands
```bash
# 1. Inspect /dev/shm for hidden high-entropy files
cd /dev/shm
ls -la

# 2. Verify Base64 encoding of the hidden archive
cat .core_dump_2025.tgz.enc

# 3. Decode the Base64 string into a standard gzip tar archive in /tmp
base64 -d /dev/shm/.core_dump_2025.tgz.enc > /tmp/stolen.tar.gz

# 4. Create a dedicated extraction folder and unpack the archive
mkdir -p /tmp/stolen_source
tar -xzvf /tmp/stolen.tar.gz -C /tmp/stolen_source
```

## Recovered Contents
* `opt/robbco/engineering/`
* `opt/robbco/engineering/MFBootAgent/`
* `opt/robbco/engineering/MFBootAgent/mfboot_main.c`
