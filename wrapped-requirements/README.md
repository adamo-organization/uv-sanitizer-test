# Wrapped requirements (LIM-44193, LIM-44140)

A requirement wrapped by `-e` or by an index option skipped the sanitizer's later rules, so it either vanished or made uv reject the file.

## Expected outcome
- `  --index-url=https://pypi.org/simple six=1.16.0` (indented, `=` spelling, single-`=` pin) → `six==1.16.0` resolves. Before: silently dropped.
- `-e idna=3.6` → `idna==3.6` resolves. Before: kept as `idna=3.6`, uv rejected the whole file.
- `urllib3 [socks]>=2.0,<3.0, --extra-index-url …` (space before extras, trailing comma) → `urllib3` 2.x and `PySocks` resolve.
- `requests==2.31.0` resolves.

LIM-48306 acceptance: the `six` line should be stored as `six` (unresolved, 1.16.0), not `index_url_six`.
