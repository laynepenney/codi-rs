# Production Readiness Remediation Plan (2026-02-11)

Tracking issue: https://github.com/laynepenney/codi/issues/294

## Goal

Bring `codi-rs` to a repeatable production baseline where any clean clone can pass build/test/lint gates, release reliably, and document the true supported state.

## Current Status (from assessment)

- `cargo build --release` succeeds.
- `cargo test` is not green from a clean clone (snapshot tests reference `insta`, but `Cargo.toml` does not include it).
- `cargo test --lib` shows at least one failing IPC transport test (`test_read_failure`).
- `cargo clippy --all-targets --all-features -- -D warnings` fails with substantial lint debt.
- CI workflows are missing (0 GitHub Actions workflows configured).
- Readiness/security/changelog docs are inconsistent with repo state.

## Production Gate Definition

`codi-rs` is considered production-ready only when all of the following are true:

1. `cargo build --release` passes on Linux, macOS, and Windows.
2. `cargo test` passes on Linux, macOS, and Windows from a clean clone.
3. Required lint/format gates pass in CI (`cargo fmt --check`, clippy policy).
4. Security disclosure/contact and changelog/release links are accurate.
5. Release process is documented and repeatable (tag -> artifact -> notes).

## Work Plan

### P0 - Stability + Reproducibility (must complete before launch)

- Fix test reproducibility blockers:
  - Add missing snapshot test dependency and lock expected versioning.
  - Stabilize/fix IPC transport failing tests (`src/orchestrate/ipc/transport.rs`).
- Add baseline CI matrix (Linux/macOS/Windows):
  - `cargo build --release`
  - `cargo test`
  - `cargo fmt --check`
  - clippy command agreed by team policy
- Make docs accurate:
  - `docs/PRODUCTION_READINESS_PLAN.md`
  - `README.md` and `SECURITY.md` contact consistency
  - `CHANGELOG.md` compare/release URLs

**Exit criteria:** Green CI matrix on default branch for 3 consecutive runs without rerun-only fixes.

### P1 - Quality Bar Hardening

- Reduce clippy debt and decide enforceable policy:
  - Option A: strict `-D warnings` for all targets
  - Option B: phased lint profile with targeted deny-list first
- Add/expand targeted tests for known fragile areas:
  - IPC error paths/timeouts
  - Windows path/process edge cases
  - snapshot redaction + formatting stability
- Add dependency/security checks in CI (`cargo-audit` or equivalent).

**Exit criteria:** Selected lint policy enforced in CI; no known flaky tests for two weeks.

### P2 - Release Operations

- Add release workflow:
  - tag validation
  - changelog enforcement
  - binary artifact packaging/signing policy
- Add operational docs:
  - rollback process
  - support matrix + known limitations
  - incident triage runbook

**Exit criteria:** One successful dry-run release plus one production release using the documented process.

## Owners and Tracking

- Primary owner: `@laynepenney`
- Tracking issue: https://github.com/laynepenney/codi/issues/294
- Subtasks: open one issue per P0 blocker; link all PRs back to tracking issue.

## Immediate Next Actions

1. Open tracking issue and link this plan.
2. Create P0 sub-issues for:
   - test dependency/reproducibility
   - IPC flaky/failing tests
   - CI matrix bootstrap
   - docs consistency corrections
3. Execute P0 in that order.
