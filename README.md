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

When `FILENAME` already ends in `$SUFFIX` and the base file without the suffix exists, it is used insted.
This allows e.g. `tsatool *.tsalog`.

Configuration variables in `tsatool` executable:
* `TSA_URL`: Trusted timestamping server
* `TSA_DELAY`: Wait at least this many seconds between server requests.
* `CERTFILE`: Local copy of all used Root CA and TSA certificates, relative to `FILENAME` (usually `tsa-certificates.crt`); automatically extended with received TSA certificates.
* `DIGEST`: Digest used in timestamp and for hashing files (usually `sha384`)
* `SUFFIX`: `$filename$SUFFIX` is where the timestamps are stored (usually `.tsalog`)

Alternatively, when a `.tsaconfig` file exists in the current directory, or any of its parents,
it's settings (`KEY=VALUE`-lines, no quotes!) override the defaults from the executable.  
When `CERTFILE` is specified there, it is treated relatively to found config file.

Requires:
* posix shell (`/bin/sh`) w/ local, getopt, wc, cut, head (-c), mktemp, dirname, (/dev/stdin,) grep, cat
* date, sleep (when `TSA_DELAY > 0`)
* openssl
* curl

Copyright (c) 2023 Tobias Hoffmann

License: https://opensource.org/licenses/MIT

