# Repository containment (LIM-44387)

The service entry must resolve requests 2.31.0, click 8.1.7 and PyYAML 6.0.1, with urllib3 constrained to 2.2.3. It follows a valid parent-directory include and a second nested include. The editable and archive entries must retain requests 2.31.0.

The extension-probe entry separately diagnoses includes whose targets use arbitrary extensions. A snapshot filter may omit .data files before analysis; a successful entry with missing packages does not pass that probe.

References to the sibling lim44387-outside directory escape the repository. The hosted scan alone cannot prove rejection when targets are missing. A controlled test must create synthetic targets outside its temporary repository, verify they exist, then run the deployed sanitizer and compare before/after uv output. Keep that directory outside this Git repository.
