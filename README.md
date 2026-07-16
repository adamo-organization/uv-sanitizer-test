# uv-sanitizer-test

Validation repo for [apiiro/lim#45590](https://github.com/apiiro/lim/pull/45590) — `PipRequirementSanitizer` transforms that normalize requirements.txt before uv sees it.

Each subdirectory is a self-contained `requirements.txt` scenario that exercises one transform. Point an Apiiro SCA scan at this repo (or any subtree) and cross-check the resulting dependency graph against the per-directory README.

## Transforms (original scope)

| Directory | Ticket | What it exercises |
|---|---|---|
| [`file-url/`](file-url/) | [LIM-42076](https://apiiro.atlassian.net/browse/LIM-42076) | Drop `file://` paths (Windows/Linux local wheels) |
| [`quoted-versions/`](quoted-versions/) | [LIM-42077](https://apiiro.atlassian.net/browse/LIM-42077) | Strip quotes around version literals (`boto3>="1.17.27"` → `boto3>=1.17.27`) |
| [`non-pep440/`](non-pep440/) | [LIM-42077](https://apiiro.atlassian.net/browse/LIM-42077) | Drop non-PEP-440 versions (`==4.0.0_unsupported`, `==0.2.0sss`) |
| [`conda-triple/`](conda-triple/) | [LIM-42078](https://apiiro.atlassian.net/browse/LIM-42078) | Rewrite `name=ver=build` conda export → `name==ver` |
| [`prose/`](prose/) | [LIM-42079](https://apiiro.atlassian.net/browse/LIM-42079) | Drop prose lines, numbered lists, bare `.py` paths |
| [`editable-local/`](editable-local/) | [LIM-42081](https://apiiro.atlassian.net/browse/LIM-42081) | Drop `-e <local-path>` (would trigger PEP 517 setup.py build) |
| [`absolute-includes/`](absolute-includes/) | [LIM-42083](https://apiiro.atlassian.net/browse/LIM-42083) | Drop `-r /abs/path` / `-c /abs/path` includes |
| [`git-plus/`](git-plus/) | [LIM-42096](https://apiiro.atlassian.net/browse/LIM-42096) | Drop `git+` URLs (`git+https`, `git+ssh`, `pkg @ git+...`) |
| [`editable-non-local/`](editable-non-local/) | [LIM-42097](https://apiiro.atlassian.net/browse/LIM-42097) | Strip `-e ` prefix from versioned pkgs; drop `-e git+url` |
| [`bare-paths/`](bare-paths/) | [LIM-42101](https://apiiro.atlassian.net/browse/LIM-42101) | Drop bare relative paths (`wheels/`); keep `.whl`/`.tar.gz` refs |
| [`comma-list/`](comma-list/) | [LIM-42102](https://apiiro.atlassian.net/browse/LIM-42102) | Expand `--no-binary a,b,c` into one flag per pkg |

## Review-fix scenarios

| Directory | Concern | What it exercises |
|---|---|---|
| [`inline-comment-noise/`](inline-comment-noise/) | @BarakSrour | `file://` and `git+` inside inline comments must not trigger drops |
| [`pep440-separators/`](pep440-separators/) | @BarakSrour | Hyphen/underscore-separated pre/post/dev + `-N` implicit post-release |
| [`chainguard-cgr/`](chainguard-cgr/) | @apiiro-adamo | Chainguard `+cgr.N` local versions + pip-compile `# via -r ...` annotation lines |

## Baseline

| Directory | Purpose |
|---|---|
| [`healthy/`](healthy/) | Sanity check — pure PEP 440 pins, sanitizer touches nothing |

## How to validate

1. Trigger a scan against this repo in a LIM environment that has `#45590` deployed.
2. For each subdirectory, compare the resulting dependency graph to the "Expected outcome" section of that directory's README.
3. `healthy/` should show the exact three deps with no sanitizer log noise.
