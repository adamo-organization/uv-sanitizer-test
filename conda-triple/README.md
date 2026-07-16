# Conda triple-pin (LIM-42078)

`conda list --export` produces `name=version=buildhash` triples. uv treats the first `=` as a comparator and rejects.

## Expected outcome
Sanitizer rewrites each triple to `pkg==version`:
- `arrow=1.1.0=pyhd8ed1ab_1` → `arrow==1.1.0`
- `numpy=1.21.0=py39h_42` → `numpy==1.21.0`
- `scikit-learn=1.0.2=py39h_x` → `scikit-learn==1.0.2`

All three resolve.
