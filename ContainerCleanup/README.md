# Container Cleanup

Clean up orphaned Docker resources that waste disk space.

## What it finds

- Orphaned volumes and networks
- Temp files from crashed containers  
- Lock files, log files, database remnants
- Dangling images and build cache

## Usage

```bash
# Download and run
curl -O https://raw.githubusercontent.com/skiptosecure/security-toolkits/main/ContainerCleanup/cleanup.sh
chmod +x cleanup.sh
./cleanup.sh
```

Shows you what's taking up space, asks before deleting anything.

## Example output

```
Found 3 orphaned volumes (taking 150MB)
Found 8 temp directories (taking 90MB) 
Remove these files? (y/N): y
CLEANED: Removed 11 items, reclaimed 240MB
```

Perfect for cleaning up after development or when disk space is low.
