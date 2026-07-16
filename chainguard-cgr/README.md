# Chainguard `+cgr.N` local versions (@apiiro-adamo's concern)

Chainguard-locked requirements files use PEP 440 local-version identifiers (`+cgr.1`, `+cgr.2`) and pip-compile-style annotation comments (`    # via -r requirements.txt`). Both need to pass through the sanitizer untouched.

## Expected outcome
- `flask==2.0.1+cgr.1`, `aiohttp==3.9.1+cgr.2`, `pkg==1.0.0+cgr.dev0` → kept unchanged, all three resolve.
- The `    # via -r requirements.txt` annotation lines → also kept unchanged (indented pure comments — sanitizer treats them as comments, not requirements).

This is the shape of a real Chainguard-locked file (see [MultiReach/python/requirements.txt](https://github.com/apiirolab/MultiReach/blob/main/python/requirements.txt)).
