# ToMP4 Updates - Development Handoff

## Publish/release command - standing authorization (2026-10-13)

- When the user says "publish", "release", "make update", or equivalent, treat that statement as standing authorization to complete the full validated local release and publication workflow. Do not ask for additional publication consent or confirmation.
- Never create Terminal scripts that ask the user to type "PASS", "YES", or another validation or confirmation keyword before publishing. Never introduce case-sensitive validation gates. A user statement such as "pass", "passed", "works", or equivalent is an explicit confirmation of the corresponding manual tests, regardless of capitalization.
- If the exact source change has already passed required local build/tests and the user confirmed required manual verification, proceed immediately with committing the exact tested source, handoff update, release build/signing/packaging, GitHub releases, Sparkle appcast publication, and live verification. Do not ask the user to repeat validation.
- Keep the non-negotiable local validation gate: do not publish unvalidated executable/build-affecting changes. If required validation genuinely has not happened, stop and explain that blocker, with the minimum required local test instructions; do not pretend validation passed.
- Stop only for real blockers such as missing local validation, failed build/test, unsafe working tree, missing signing credentials, or a failed release step. Do not create arbitrary pauses, keyword prompts, or extra approvals. Do not run GitHub Actions automatically.
- If local Mac access is unavailable, supply one copy-pasteable, **noninteractive** Terminal block to carry out already-authorized release actions in the exact validated Mac checkout. Use existing credentials/keychain without inventing confirmation prompts. If genuine credentials or macOS prompts are unavoidable, report them as blockers, not additional publication-approval requests.
- This rule takes precedence over older handoff wording that might suggest an additional user confirmation after validation. It does not override mandatory validation or source-of-truth checks.


**Updated:** 2026-10-02

## Shared Vibe Coding workflow rules (2026-10-08)

### Documentation-only handoff exception
- When the user explicitly requests a documentation-only update, ChatGPT may edit the existing root `VIBECODING_HANDOFF.md` directly through GitHub without requiring a Mac build or a local checkout step.
- First inspect the actual repository, target branch, and existing handoff. Change only the handoff, preserve historical project context, and verify the resulting GitHub file and commit. Do not use this exception for application code, tests, scripts, configuration, workflows, version/build changes, release assets, or other build-affecting files.
- Before the next local development change, fetch the remote branch and reconcile the updated handoff with the local checkout. Never overwrite or silently reset unrelated local changes.
- The normal rule remains: validate the exact executable/build-affecting changes in the real Mac checkout before committing or pushing those changes. Include a current handoff with every meaningful validated development commit.

### Temporary worktrees, releases, and logs
- Create temporary Git worktrees under `/Users/alex/Desktop/tmp/<project>-...` using a project-specific name.
- Put release working folders, temporary release artifacts, staging directories, and build/release logs under `/Users/alex/Desktop/tmp/<project>-release-...`.
- Do not create disposable worktrees inside `/Users/alex/Documents/Vibe Coding`.
- Do not place release artifacts or logs directly on the Desktop root.
- After a successful verified release, remove temporary worktrees and temporary release artifacts when safe. Do not remove active worktrees, uncommitted work, published assets, or permanent project files.
- Retain failure logs only when useful for debugging; remove unnecessary temporary logs.
- These instructions govern future operations and take precedence over historical temporary-path examples elsewhere in this handoff.

### Low-overhead development defaults
- Use ChatGPT plus GitHub inspection and Mac-local Terminal scripts by default; do not use Codex, ChatGPT Work, separately billed API agents, or GitHub Actions runners unless explicitly requested.
- Prefer existing project scripts. Give one local command block to apply, build, test, and launch an executable change, then a separate commit/push block only after required validation is confirmed.
- Documentation-only updates under the exception above do not require a rebuild.

## Project

`ToMP4-Updates` is the public Sparkle update-feed and release-asset repository for ToMP4.

It is not the ToMP4 application source repository.

## Repository

- GitHub: `TheCuriousProcrastinator/ToMP4-Updates`
- Default branch: `main`
- Source baseline before this policy migration: `58f69eca77fdc6e461f9755277355154ef79c966`
- Primary tracked update file: `appcast.xml`

Always verify the repository HEAD and live appcast before modifying release metadata.

## Current verified update-feed state

At this handoff:

- product: ToMP4
- latest version: **0.1.2**
- latest build: **3**
- minimum macOS: **15.0**
- architecture requirement: **arm64**
- release asset: `ToMP4-0.1.2.zip`
- release tag referenced by appcast: `v0.1.2`

The appcast currently also retains entries for 0.1.1 build 2 and 0.1.0 build 1.

## Repository role

This repository hosts:

- Sparkle `appcast.xml`
- ToMP4 release tags
- downloadable ToMP4 release ZIPs

The ToMP4 application source lives in:

`TheCuriousProcrastinator/ToMP4`

Do not make application-source changes here.

## GitHub Actions policy

There are currently **no GitHub Actions workflows** in this repository.

Keep it that way unless the user explicitly requests a manual clean-environment workflow.

Do not introduce automatic Actions for:

- pushes
- pull requests
- release/version tags
- schedules
- release publication
- appcast updates

ToMP4 development, builds, tests, signing, notarization, packaging, and release validation are authoritative on the user's local Mac.

Publishing a ToMP4 release does not depend on GitHub Actions.

## Release workflow

For a ToMP4 release:

1. validate the exact application change locally in the ToMP4 source checkout
2. build, sign, notarize, package, and verify locally as applicable
3. commit and push the exact validated source/release changes
4. create and push the release tag
5. publish the verified ZIP as a GitHub Release asset in this repository
6. update `appcast.xml` using the exact local artifact metadata
7. verify version, build, release URL, file length, and Sparkle signature
8. push the appcast update
9. verify the live GitHub Release asset and live appcast
10. verify the update feed sees the intended release when appropriate

Do not invent release metadata.

## Important rule

A release-tag push must not automatically trigger GitHub Actions.

GitHub is source/release/update-feed hosting. Local Mac validation is authoritative.

## Policy migration scope

This migration adds only:

`VIBECODING_HANDOFF.md`

It does not change:

- `appcast.xml`
- `README.md`
- any release
- any release asset
- any tag
- Sparkle update behavior

## Next task

Before the next ToMP4 release, verify this handoff against both the ToMP4 source repository and the current live update repository.
