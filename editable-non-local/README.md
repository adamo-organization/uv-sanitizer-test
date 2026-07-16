# `-e` with non-local-directory target (LIM-42097)

uv enforces that `-e` must point at a local directory. pip historically tolerated `-e <package>==<version>` (no-op) and `-e git+url`. When customers use these shapes, uv aborts the compile.

## Expected outcome
- `-e pytest`, `-e pytest==7.0.0`, `--editable somepkg==1.0` → sanitizer strips the `-e ` prefix, leaving `pytest`, `pytest==7.0.0`, `somepkg==1.0` — all resolve.
- `-e git+https://...` → dropped entirely (git URL, unreachable).
- `requests==2.31.0` and `flask==3.0.0` resolve.
