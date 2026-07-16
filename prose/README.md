# Prose / source paths (LIM-42079)

Files named `requirements.txt` that aren't actually pip requirements — README-style prose, numbered lists, bare Python source paths.

## Expected outcome
Sanitizer drops the numbered/prose lines, the bare `.py` paths, and leaves only `requests==2.31.0` and `flask==3.0.0` for uv.
