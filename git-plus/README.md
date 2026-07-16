# git+ URL requirements (LIM-42096)

git+ URLs frequently break uv — missing subdirectories, private repos with no token, unreliable network. Analyzer can't reliably resolve them.

## Expected outcome
Sanitizer drops all three git+ URLs (bare, `@`-referenced, `git+ssh`). `requests==2.31.0` and `flask==3.0.0` resolve.
