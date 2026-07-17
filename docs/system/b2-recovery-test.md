# Backblaze B2 Recovery Test

Date: 2026-07-17

## Storage

- rclone remote: `b2-archive:`
- Backblaze bucket: `wetlands-archive-raw`
- Test object: `infrastructure-tests/2026-07-17/b2-archive-test.txt`

## Procedure

1. Created a local test file.
2. Uploaded it to Backblaze B2 using rclone.
3. Verified the remote object using `rclone check`.
4. Deleted the local source copy.
5. Restored the object from Backblaze B2.
6. Compared the restored SHA-256 checksum with the original.

## Checksum

`89df4e2cb90ad7e6e8230f2cb4ec6eb5293d8d3e28158b7fc61dc17ec94be5c0`

## Result

PASS — the restored file matched the original exactly.
