# file:// URL strip (LIM-42076)

Local Windows/Linux `file://` wheel paths that only exist in the customer's build env. Sanitizer drops any line containing `file://` (regardless of position — bare `file://...whl`, `pkg @ file://...`, `-r file://...`, `-e file://...`).

## Expected outcome
Only `requests==2.31.0` and `flask==3.0.0` end up in the dependency graph. All six `file://` lines are silently dropped by the sanitizer before uv sees them.
