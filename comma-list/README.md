# `--no-binary` / `--only-binary` comma list (LIM-42102)

pip accepts `--no-binary pkg1,pkg2,pkg3`. uv requires one flag per package. Single comma list → whole file rejected.

## Expected outcome
- `--no-binary numpy,spacy,blis,thinc,cymem` → expanded to five `--no-binary <pkg>` lines.
- `--only-binary pkg1,pkg2` → expanded to two lines.
- `--no-binary :all:` and `--no-binary singlepkg` → kept unchanged (no comma).
- `requests==2.31.0` and `flask==3.0.0` resolve.
