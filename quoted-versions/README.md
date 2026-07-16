# Quoted version literals (LIM-42077 — quoted variant)

Some tools export requirements with quoted version numbers (`boto3>="1.17.27"`). pip tolerates this; uv rejects with `expected version to start with a number, but no leading ASCII digits were found`.

## Expected outcome
Sanitizer strips the quotes, resulting in `boto3>=1.17.27`, `requests==2.28.1`, `Flask<=3.0.0`. All three resolve successfully.
