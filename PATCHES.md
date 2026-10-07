# Patches

This repository is a public fork of
[MaxApiTeam/PyMax](https://github.com/MaxApiTeam/PyMax) starting from tag
`v2.4.1` (commit `53103f0`).

## Version

- Package / dist name: `pymax`
- Import name: `pymax` (unchanged)
- Version: `2.4.1+fork.1` (PEP 440 local version)

## Applied changes

### Photo upload token extraction (upstream PR #107)

Upstream commit series ending at `433d096` /

[PR #107](https://github.com/MaxApiTeam/PyMax/pull/107):

- File: `src/pymax/api/uploads/service.py`
- Do not require a `photoIds` query parameter on the upload URL before POST.
- After POST, extract the token from the single entry in the `photos` map via
  `_extract_photo_token`.
- Raise `UploadError` if the response contains 0 or more than 1 photo.
- Regression tests in `tests/api/test_upload_service.py`.

### Metadata

- Homepage / repository URLs point at https://github.com/smart-art/pymax
- Package name set to `pymax` for this repository
- MIT license retained from upstream
