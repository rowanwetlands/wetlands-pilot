# Current Project Architecture

Recorded: 2026-07-17T13:49:28+01:00

## Repository

```text
Local path: /home/rowan/Documents/wetlands-pilot
Branch: main
Commit: 084bde235f8064d7510ad7f8f25a8314daa78500

Git remotes:
origin	https://github.com/rowanwetlands/wetlands-pilot.git (fetch)
origin	https://github.com/rowanwetlands/wetlands-pilot.git (push)

Tags:
infrastructure-v0.1.0
```

## DVC

```text
r2store s3://wetlands-raw-rowan/dvc     (default)

[core]
    remote = r2store
['remote "r2store"']
    url = s3://wetlands-raw-rowan/dvc
    endpointurl = https://cab49a864db2c8fd50aa7f24700ed043.r2.cloudflarestorage.com

Credential file ignore rule:
.dvc/.gitignore:1:/config.local	.dvc/config.local
```

## Storage

```text
Cloudflare R2:
  wetlands-raw-rowan/dvc — current DVC remote
  raw — reserved
  products — reserved

Backblaze B2:
  wetlands-archive-raw — created but not configured

Compute:
  Local Linux Mint machine
  No external CPU worker
  No GPU worker
  No Docker container
```

## Current status

- Git and GitHub tested.
- DVC and R2 tested.
- Clean restore has not yet been tested.
- B2 backup has not yet been tested.
- No real research data have been acquired.
