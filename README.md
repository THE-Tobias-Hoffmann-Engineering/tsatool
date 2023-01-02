# tsatool
## Manage append-only files secured with a trusted timestamp.

Usage:
```
tsatool init [-f] NEW_FILENAME...
  -f: Instead of creating an empty file itself, start with existing one (possibly not empty).

tsatool FILENAME...
  Add new timestamping record for any data added since last invocation.
  When no data is added, no new record is created
  (the file's completeness is still checked against the last record, though).

tsatool verify [-a] FILENAME...
  -a: Check all intermediate hashes + timestamps, not just the final one.
```

Configuration variables in `tsatool` executable:
* `TSA_URL`: Trusted timestamping server
* `CAPATH`: Local copy of all used root certificates
* `DIGEST`: Digest used in timestamp and for hashing files (usually `sha384`)
* `SUFFIX`: `$filename$SUFFIX` is where the timestamps are stored (usually `.tsalog`)

Requires:
* posix shell (`/bin/sh`), getopt, wc, cut, head (-c), mktemp, /dev/stdin
* openssl
* curl

Copyright (c) 2023 Tobias Hoffmann

License: https://opensource.org/licenses/MIT

