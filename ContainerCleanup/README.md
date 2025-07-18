# Container Cleanup

A comprehensive bash script for detecting and cleaning orphaned Docker resources that accumulate over time in development and production environments.

## Overview

When containers are destroyed improperly or applications crash, they often leave behind orphaned resources that consume disk space and clutter your system. Container Cleanup helps you identify exactly what's been left behind and provides safe, interactive cleanup options.

## What It Detects

Container Cleanup scans for 10 types of commonly orphaned resources:

1. **Orphaned Docker volumes** - Unused volumes taking up disk space
2. **Orphaned Docker networks** - Custom networks no longer in use
3. **Temp files in bind mounts** - Large files left in `/tmp` and mounted directories
4. **Named pipes and sockets** - IPC mechanisms left by crashed containers
5. **Lock and PID files** - Process control files from terminated containers
6. **Database data directories** - PostgreSQL and other database remnants
7. **Large log files** - Runaway application logs consuming disk space
8. **Shared memory files** - Files left in `/dev/shm` by containers
9. **Background process work files** - Files from daemon processes and workers
10. **Dangling Docker images** - Unused image layers and build artifacts

## The Script

### `dockercleanup.sh`
Comprehensive cleanup script that:
- Scans your system for all 10 types of orphaned resources
- Shows detailed information about what was found
- Calculates disk space usage for each category
- Provides interactive prompts for destructive operations
- Reports exactly what was cleaned and how much space was reclaimed

## Installation

1. Download the script:
```bash
curl -O https://your-repo/dockercleanup.sh
```

2. Make it executable:
```bash
chmod +x dockercleanup.sh
```

## Usage

### Quick Start
```bash
# Clean up orphaned resources
./dockercleanup.sh
```

### Regular Maintenance
```bash
# Run cleanup to identify and remove orphaned resources
./dockercleanup.sh
```

The cleanup script will:
- Show you exactly what orphaned resources exist
- Ask for confirmation before removing anything destructive
- Provide detailed reporting of what was cleaned
- Display before/after system status

## Sample Output

```
Starting container cleanup scan...

1. Scanning for orphaned volumes...
   Found 3 orphaned volumes:
   - orphan-cache-vol-1752879369
   - orphan-db-vol-1752879369
   - orphan-logs-vol-1752879369
   CLEANED: Removed 3 orphaned volumes

2. Scanning for orphaned networks...
   Found 2 orphaned networks:
   - orphan-backend-net-1752879369 (b2a13d0ff288)
   - orphan-frontend-net-1752879369 (c96cdba5549a)
   CLEANED: Removed 2 orphaned networks

...

==========================================
CLEANUP SUMMARY
==========================================
Total items cleaned: 18
Total disk space reclaimed: 90MB
```

## Safety Features

- **Interactive prompts** for potentially destructive operations
- **Detailed preview** of what will be deleted before confirmation
- **Graceful error handling** - script continues even if individual operations fail
- **Read-only scanning** - shows problems without making changes until you confirm
- **Comprehensive logging** of all cleanup actions

## System Requirements

- Linux/Unix environment
- Docker installed and accessible
- Bash 4.0+
- Standard Unix utilities: `find`, `du`, `df`, `lsof`
- Sufficient permissions to clean `/tmp` and Docker resources

## Common Use Cases

### Development Environment Cleanup
Run after development sessions to clean up orphaned containers and volumes:
```bash
./dockercleanup.sh
```

### CI/CD Pipeline Maintenance
Integrate into build pipelines to prevent resource accumulation:
```bash
# Add to your CI cleanup stage
./dockercleanup.sh
```

### Production System Maintenance
Schedule regular cleanup to prevent disk space issues:
```bash
# Add to crontab for weekly cleanup
0 2 * * 0 /path/to/dockercleanup.sh
```

### Troubleshooting Disk Space
When you're running out of disk space and suspect container orphans:
```bash
./dockercleanup.sh
```

## Understanding the Output

The script provides detailed metrics for each cleanup category:

- **Items found** - Count of orphaned resources discovered
- **Disk space usage** - How much space each category is consuming
- **Cleanup results** - Exactly what was removed and space reclaimed
- **System status** - Before/after comparison of Docker and filesystem usage

## Contributing

This is a bash script for container maintenance. To contribute:

1. Test thoroughly in isolated environments
2. Ensure compatibility with major Linux distributions
3. Add error handling for edge cases
4. Update documentation for any new cleanup categories

## License

MIT License - feel free to use and modify for your needs.

## Troubleshooting

### Script hangs during cleanup
- Check for permission issues in `/tmp`
- Ensure Docker daemon is running
- Verify no processes are using files being cleaned

### "Permission denied" errors
- Run with appropriate sudo permissions for system cleanup
- Check Docker group membership for Docker operations

### False positives in detection
- The script errs on the side of safety - review findings before confirming cleanup
- Some "orphaned" resources may be legitimately in use by stopped containers

## Why This Matters

Container environments can accumulate significant amounts of orphaned resources over time:
- **Development environments** commonly have 40-60% orphaned resources
- **Production systems** typically see 5-15% orphaned resources
- **Unmanaged systems** can waste hundreds of GB on orphaned data

Regular cleanup prevents disk space issues, improves performance, and maintains a clean container environment.
