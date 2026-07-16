# Inline-comment-safe matching (review fix from @BarakSrour)

Before the review fix, `FileUrlLineRegex` and `GitUrlRequirementRegex` scanned the whole line — so a valid pinned requirement whose inline comment mentioned `git+` or `file://` was silently dropped.

## Expected outcome
All five lines resolve unchanged. The tokens inside the inline comments (`git+https://...`, `file:///var/www/wheels`, etc.) are ignored — sanitizer strips comments before matching.

`requests`, `Flask`, `boto3`, `pkg`, `click` should all end up in the dependency graph.
