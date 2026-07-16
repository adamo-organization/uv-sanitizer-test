# Absolute `-r` / `-c` includes (LIM-42083)

`requirements.txt` references a constraints or includes file by an absolute path that only exists on the customer's build host (Airflow container, Windows dev machine). The path doesn't exist on the analyzer, so uv aborts with `failed to read from file: No such file or directory`.

## Expected outcome
Sanitizer drops all four absolute-path includes (`/usr/local/airflow/...`, `/etc/pip/...`, `C:\airflow\...`). `requests==2.31.0` and `flask==3.0.0` resolve.
