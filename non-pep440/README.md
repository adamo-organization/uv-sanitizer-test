# Non-PEP-440 version pins (LIM-42077 — garbage-suffix variant)

Versions with a garbage tail after a valid version number. pip tolerates; uv rejects the whole compile.

## Expected outcome
The three garbage-suffix lines (`pyodbc==4.0.0_unsupported`, `google-pasta==0.2.0sss`, `click==8.1.7garbage`) are dropped. `requests==2.31.0` and `flask==3.0.0` resolve.
