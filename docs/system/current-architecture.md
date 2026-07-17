# Current Project Architecture

Recorded: 2026-07-17T13:41:10+01:00

## Project

```text
Repository directory: /home/rowan/Documents/wetlands-pilot
GitHub repository:
origin	https://github.com/rowanwetlands/wetlands-pilot.git (fetch)
origin	https://github.com/rowanwetlands/wetlands-pilot.git (push)

Current Git branch:
main

Current Git commit:
5236a4e8318f95ddcb05dc578b6a7750b5c49e2f

Current Git tags:
infrastructure-v0.1.0
```

## DVC and Cloudflare R2

```text
Configured DVC remotes:
r2store s3://wetlands-raw-rowan/dvc     (default)

Tracked DVC configuration:
[core]
    remote = r2store
['remote "r2store"']
    url = s3://wetlands-raw-rowan/dvc
    endpointurl = https://cab49a864db2c8fd50aa7f24700ed043.r2.cloudflarestorage.com

Local credential file ignore rule:
.dvc/.gitignore:1:/config.local	.dvc/config.local
```

The DVC remote currently uses the Cloudflare R2 bucket:

```text
wetlands-raw-rowan/dvc
```

This is confirmed working but is intended to move later to a dedicated DVC bucket.

## Current storage architecture

```text
GitHub
  Code, documentation, configuration and DVC pointer files

Cloudflare R2
  Bucket: wetlands-raw-rowan
    /dvc/      Current DVC content-addressed cache
    /raw/      Reserved for original source data
    /products/ Reserved for derived products

Backblaze B2
  Bucket: wetlands-archive-raw
  Status: not yet connected or tested

Compute
  Local Linux Mint workstation
  Ephemeral CPU worker: not yet provisioned
  Ephemeral GPU worker: deferred
  Docker environment: not yet created
```

## Host system

```text
Linux rowan-MacBook 6.14.0-29-generic #29~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Thu Aug 14 16:52:50 UTC 2 x86_64 x86_64 x86_64 GNU/Linux
x86_64
NAME="Linux Mint"
VERSION="22.2 (Zara)"
ID=linuxmint
ID_LIKE="ubuntu debian"
PRETTY_NAME="Linux Mint 22.2"
VERSION_ID="22.2"
HOME_URL="https://www.linuxmint.com/"
SUPPORT_URL="https://forums.linuxmint.com/"
BUG_REPORT_URL="http://linuxmint-troubleshooting-guide.readthedocs.io/en/latest/"
PRIVACY_POLICY_URL="https://www.linuxmint.com/"
VERSION_CODENAME=zara
UBUNTU_CODENAME=noble

Python 3.12.3
aws-cli/1.45.50 Python/3.12.3 Linux/6.14.0-29-generic botocore/1.43.50
DVC version: 3.67.1 (pip)
-------------------------
Platform: Python 3.12.3 on Linux-6.14.0-29-generic-x86_64-with-glibc2.39
Subprojects:
	dvc_data = 3.18.3
	dvc_objects = 5.2.0
	dvc_render = 1.0.2
	dvc_task = 0.40.2
	scmrepo = 3.6.2
Supports:
	http (aiohttp = 3.14.1, aiohttp-retry = 2.9.1),
	https (aiohttp = 3.14.1, aiohttp-retry = 2.9.1),
	s3 (s3fs = 2026.6.0)
Config:
	Global: /home/rowan/.config/dvc
	System: /etc/xdg/xdg-xfce/dvc
Cache types: hardlink, symlink
Cache directory: ext4 on /dev/nvme0n1p2
Caches: local
Remotes: s3
Workspace directory: ext4 on /dev/nvme0n1p2
Repo: dvc, git
Repo.site_cache_dir: /var/tmp/dvc/repo/5c89d77a27ba317de929887d8f8e17a8
git version 2.43.0
gh version 2.45.0 (2025-07-18 Ubuntu 2.45.0-1ubuntu0.3)
https://github.com/cli/cli/releases/tag/v2.45.0

Filesystem      Size  Used Avail Use% Mounted on
tmpfs           784M  1.8M  783M   1% /run
/dev/nvme0n1p2  458G   43G  392G  10% /
tmpfs           3.9G  4.0K  3.9G   1% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
/dev/nvme0n1p1  511M  6.2M  505M   2% /boot/efi
tmpfs           784M  2.5M  782M   1% /run/user/1000
```

## Current completion status

- Git repository initialized and pushed to GitHub.
- GitHub CLI browser authentication configured.
- DVC initialized.
- DVC S3 support installed.
- Cloudflare R2 remote tested successfully.
- DVC pointer-to-object workflow tested.
- Infrastructure milestone tagged as infrastructure-v0.1.0.
- Backblaze B2 backup not yet configured.
- No real project datasets acquired.
- Docker deferred until the first real processing pipeline exists.
