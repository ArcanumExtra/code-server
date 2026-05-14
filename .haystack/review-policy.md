# Review Policies

## Manual review for workflow and CI pipeline edits
- **Paths**: `.github/workflows/**`, `ci/build/**`
- **Severity**: high
- **Reason**: Workflow/CI edits can silently change release behavior, required checks, cache semantics, and credential usage; passing checks do not guarantee the pipeline still enforces the intended safety and reproducibility constraints.

## Manual review for authentication and session routing changes
- **Paths**: `src/node/**`
- **Severity**: critical
- **Reason**: Auth, cookie/session, proxy, and request-handling logic can introduce security regressions or lockouts that static checks may miss, especially around header behavior, credential validation, and proxy host handling.

## Manual review for upstream patch diffs
- **Paths**: `patches/**/*.diff`
- **Severity**: high
- **Reason**: Patch files can accidentally include shifted or unrelated hunks and may break upstream merge assumptions; reviewers must verify semantic intent against upstream code, not just passing tests.

## Instructions
- If a change alters CI cancellation behavior, a human should judge whether faster feedback is worth losing full failure visibility, cache uploads, or fork compatibility.
- If a change modifies automatic proxy URI derivation or placeholder semantics, require human review to confirm behavior is correct across sub-path deployments, forwarded hosts, and custom proxy topologies.
- If a change makes authentication mode selection implicit (or changes when credentials are auto-applied), a human must validate backward compatibility and future extensibility tradeoffs.
