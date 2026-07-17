# DVC Recovery Test

Date: 2026-07-17

## Test

A fresh clone of the GitHub repository was created at:

`~/Documents/wetlands-pilot-restore-test`

The DVC-managed `test.txt` file was restored from the dedicated Cloudflare R2 bucket:

`wetlands-dvc-rowan/dvc`

## Result

The restored file contained:

`hello wetlands`

SHA-256:

`4dcaa06be099df87b20f0c687d1c33c1c319594dc53f5f382a4a1c3961e9abe7`

The checksum matched the original exactly.

## Status

PASS — GitHub and Cloudflare R2 can jointly restore the project record and DVC-managed data.
