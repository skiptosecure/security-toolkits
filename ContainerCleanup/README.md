# Container Cleanup

Clean up orphaned Docker resources that waste disk space.

## What it finds

Orphaned Docker volumes - Unused volumes taking up disk space
Orphaned Docker networks - Custom networks no longer in use
Temp files in bind mounts - Large files left in /tmp and mounted directories
Named pipes and sockets - IPC mechanisms left by crashed containers
Lock and PID files - Process control files from terminated containers
Database data directories - PostgreSQL and other database remnants
Large log files - Runaway application logs consuming disk space
Shared memory files - Files left in /dev/shm by containers
Background process work files - Files from daemon processes and workers
Dangling Docker images - Unused image layers and build artifacts

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
