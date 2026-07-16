# Local editable entries (LIM-42081)

`-e <local-path>` triggers uv's PEP 517 build backend, which invokes the project's `setup.py`. In the analyzer environment those setup scripts commonly `open("README.md")` or similar and fail with `FileNotFoundError`. uv exits 2 and the whole compile is lost.

## Expected outcome
Sanitizer drops all four `-e <path>` lines. `requests==2.31.0` and `flask==3.0.0` resolve.
