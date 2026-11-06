# Changelog

All notable changes to the PowPow Claude Code plugin are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-11-06

### Added

- PowPow remote MCP server (`powpow`) over streamable HTTP at
  `https://global.powpow.online/api/mcp`, with OAuth 2.1 + PKCE and dynamic
  client registration.
- 34 tools exposed: 20 read-only (nearby discovery, account, posts, campaigns)
  and 14 write (publish, like, follow, favorite, reply, digital humans).
- `powpow-register` skill: guided PowPow account sign-up, email verification
  and subscription activation, so a new user can get from zero to a working
  connection without leaving the conversation.
- Bilingual README (Chinese first) covering installation on Claude Code,
  claude.ai and Cowork, the full network destination list, rate limits and the
  two-step write safeguards.

### Notes

- Writing is always two-step: the server drafts first and publishes only after
  the user confirms.
- Content created through the assistant can be undone through the assistant
  within 24 hours.
- The three public search tools (`find_nearby`, `geocode_place`,
  `nearby_attractions`) are limited to 12 calls per 60 seconds per access
  token; all other tools are unlimited.

[1.0.0]: https://github.com/durenzidu/powpow-claude-plugin/releases/tag/v1.0.0
