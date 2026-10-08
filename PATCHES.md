# Patches

This repository is a public fork of
[MaxApiTeam/PyMax](https://github.com/MaxApiTeam/PyMax) starting from tag
`v2.4.1` (commit `53103f0`).

## Version

- Package / dist name: `pymax`
- Import name: `pymax` (unchanged)
- Version: `2.4.1+fork.2` (PEP 440 local version)

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

### Link preview control (`detectShare`)

- Files: `src/pymax/api/messages/payloads.py`, `src/pymax/api/messages/service.py`,
  `src/pymax/infra/message.py`, `src/pymax/types/domain/message.py`,
  `src/pymax/types/domain/chat.py`
- `SendMessagePayloadMessage` gains `detect_share: bool | None`, serialized
  as `message.detectShare` (omitted when `None`). Official MAX clients send this
  flag on every outgoing message; when it is true the server detects a URL in
  the text and attaches a link preview (`SHARE` attach).
- `send_message(..., link_preview=...)` (service + `Client`) and the bound
  helpers `Message.reply`, `Message.answer`, `Chat.answer` pass it through.
  `link_preview=False` → `detectShare: false` (no preview card);
  `True` → `detectShare: true`; `None` (default) → field omitted, server default.
- Tests in `tests/api/test_message_service.py`.

### Metadata

- Homepage / repository URLs point at https://github.com/smart-art/pymax
- Package name set to `pymax` for this repository
- MIT license retained from upstream

### CI workflows

Upstream GitHub Actions under `.github/workflows/` were omitted from this
fork so the initial push does not require the OAuth `workflow` scope.
Re-add CI later if desired.

