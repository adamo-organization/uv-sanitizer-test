# Bare relative paths (LIM-42101)

Lines that are just a path — no PEP 508 version pin. uv treats them as URLs and fails with `Invalid URL: relative URL without a base`.

## Expected outcome
- `wheels/`, `packages/wheels`, `./local/dir/` → dropped by the sanitizer (no valid archive extension).
- `requests==2.31.0` and `flask==3.0.0` resolve.

## Note on the "keep archive extensions" side of this transform
The sanitizer intentionally keeps bare paths that end in `.whl` / `.tar.gz` / `.zip` etc. (they're valid direct file references in PEP 508). That behavior is unit-tested in `PipRequirementSanitizerTests` — not exercised here because uv would then try to fetch the archive from disk and fail with `Distribution not found at: file:///...` when the file doesn't actually exist in the repo. Testing that path end-to-end would require committing real archive files, which is out of scope for this validation repo.
