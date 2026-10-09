# Project Separation History

## Decision

On 2026-10-09, the WeChat Official Account Markdown editor was separated from `codex-feishu-automation-kit` into the public repository `helloLeila/WeChat-Markdown-Convert-Editor`. The Feishu / Server 酱 automation toolkit remains in its original repository.

The separation was requested because the two tools had unrelated purposes and were sharing one README, package manifest, test suite, and Docker deployment setup. The editor now has its own startup command, dependencies, tests, deployment assets, and documentation.

## Migrated Project History

The standalone repository contains the editor source, tests, Docker assets, status/design documentation, and these implementation records:

- `docs/superpowers/plans/2026-08-20-wechat-editor-prototype.md`
- `docs/superpowers/plans/2026-09-04-wechat-editor-production.md`
- `docs/superpowers/plans/2026-09-14-wechat-config-links.md`
- `docs/superpowers/plans/2026-09-18-wechat-editor-production-sync.md`
- `docs/superpowers/specs/2026-07-13-open-wechat-editor-design.md`
- `docs/superpowers/specs/2026-08-20-wechat-sync-config-design.md`
- `docs/superpowers/specs/2026-09-14-wechat-config-links-design.md`
- `docs/superpowers/specs/2026-09-18-wechat-editor-production-sync-design.md`

Eleven editor-related Git commits were filtered from the original repository and connected to the standalone repository history. Feishu files were not included in that filtered history.

## Repository Cleanup

The editor was removed from the original repository's default branch while its old commits remain in the original Git history:

- PR #2 removed the editor source, deployment setup, tests, and editor-specific docs from the default branch.
- PR #3 removed the final editor status document.

## Verification

At separation time, the standalone editor passed all 84 tests, its resource build, and syntax checks. The Feishu-focused branch passed its syntax checks, 50 tests, and dry-run formatting check. The clean default-branch removal PR passed syntax and dry-run checks; one unrelated readiness-panel assertion failed among 47 tests on the original `main` baseline.

This file records project decisions and repository history. It is not a verbatim export of private chat transcripts.
