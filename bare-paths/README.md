# Bare relative paths (LIM-42101)

Lines that are just a path — no PEP 508 version pin. uv treats them as URLs and fails with `Invalid URL: relative URL without a base`.

## Expected outcome
- `wheels/`, `packages/wheels`, `./local/dir/` → dropped (no valid archive extension).
- `./dist/my_pkg-1.0.0-py3-none-any.whl`, `dist/pkg.tar.gz` → **kept** (valid archive extensions — supported by uv as direct file references).
- `requests==2.31.0` and `flask==3.0.0` resolve.
