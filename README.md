# OSBackup

## ObjectStorage Backup / OpenSource Backup

A system optimized to backup files to Amazon S3, natively
It will be upgraded in the near future to also support other systems such as Google Cloud Storage or Azure Cloud File storage.

## Why this system?

When I decided to write this tool, all of the opensource systems (that I know of) are often made for single servers - or for tapes. This means using things like VTL (virtual tape library) combined with Bacula, which is complex and relatively expensive (inefficiency in storage + paying the actual VTL + handle a server)

This system directly connects to S3

## What is the OSBackup system?

It's a series of command line tools and a structure to store files easily.
It creates a catalog (list of backed up files) and a series of tarball files and uploads them to S3.
If it's a differential backup, it downloads the previous catalog, calculates at the difference, then uploads only the files that have changed since last time.

It also has a restore function that will either restore in place, or restore in another directory (recommended) to allow you to pick which files to recover.

## How to set it up?

Storage:
- Create Amazon S3 account (or use existing)
- Create S3 bucket (or use existing)
- Create S3 IAM user with API keys (or use existing)

OSBackup:
- Download OSBackup binary to server
- Create configuration file
- Set up cronjob (or any trigger method you want) to run OSBackup regularly

All the OSBackup part can be done via configuration management such as a chef cookbook, ansible, etc.

## What if...

I have several servers:
- Use configuration management
- Space out the cron jobs or use centralized triggered such as Rundeck

I want to back up an SQL database:
- Dump it and backup the dump file
- Do a partition snapshot and backup that partition

I want consistent backups:
- Use snapshots
- Stop the running processes (yeah ok use snapshots)
