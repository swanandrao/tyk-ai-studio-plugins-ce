# Changelog

## [0.1.2] - 2026-10-27

### Added

- Hosted autochunk delivery for oversized eligible context. The hosted Select
  API owns chunking, while the adapter preserves original provider message
  order, roles, and tool identifiers when it restores selected excerpts.
- Digest-pinned, signed OCI image for `linux/amd64` and `linux/arm64`.
- Request-side selection, scan/quarantine, enforce-mode blocking, and
  content-free gateway receipts through Tyk AI Studio's `post_auth` hook.
