# Repository containment (LIM-44387)

Each entry requirements.txt must resolve requests 2.31.0. The service scenario must also resolve click 8.1.7 and PyYAML 6.0.1, with urllib3 constrained to 2.2.3. It follows a valid parent-directory include, a nested include with an arbitrary extension.

References to the sibling `lim44387-outside` directory escape the repository. They must not contribute outside-demo or outside-only packages. The hosted scan alone cannot prove rejection when those targets are missing. The controlled test must create synthetic targets outside its temporary repository before running the deployed sanitizer, verify they exist, and compare the before/after contents. Keep that directory outside this Git repository.
