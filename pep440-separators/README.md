# PEP 440 separator variants (review fix from @BarakSrour)

PEP 440 normalizes `-`, `_`, and `.` as equivalent separators before pre/post/dev segments, plus the implicit `-N` post-release form. uv accepts all of these; the earlier version regex only accepted the `.` variant and dropped the rest.

## Expected outcome
All nine lines pass sanitizer validation as-is (unchanged) and are handed to uv:
- Hyphen/underscore-separated pre-releases (`1.0.0-beta`, `1.0.0_rc1`)
- Implicit post-release (`1.0-1`)
- Alternative separators for post/dev (`1.0_post1`, `1.0-dev1`)
- The already-accepted `.`-separated forms (control)
- Wildcards and epochs (`1.0.*`, `1!2.0`) — accepted since the last review.

Whether they *resolve* against a real index is a separate question — the packages here are stubs. The point of this test is that the sanitizer doesn't drop them as "invalid PEP 440."
