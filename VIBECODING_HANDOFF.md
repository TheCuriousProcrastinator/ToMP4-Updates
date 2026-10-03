# ToMP4 Updates - Development Handoff

**Updated:** 2026-10-02

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
