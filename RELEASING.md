# Releasing Specsmith

This document is the single source of truth for cutting a release: how to choose
the version number, the steps to publish, and the template for the release notes.
Everything user-facing — tags, titles, release notes — is written in **English**.

## Versioning — Semantic Versioning

Specsmith follows [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).
A version is `MAJOR.MINOR.PATCH` (e.g. `0.1.0`).

The "public surface" of Specsmith is what users depend on: the skill **names and
invocation**, the **spec → plan → tasks → kickoff → close flow contract**, the
`specs/` **scaffold layout and template structure**, and the **plugin/marketplace
manifests**. Bumps are decided against that surface.

| Bump | When | Examples |
|---|---|---|
| **MAJOR** (`X.0.0`) | A backward-incompatible change to the public surface. | Removing or renaming a skill; changing a skill's invocation name; breaking the flow contract or the scaffold layout so existing usage no longer works. |
| **MINOR** (`0.X.0`) | New, backward-compatible functionality. | Adding a new skill or template; adding an optional capability or flag; extending a skill's behavior without breaking current usage. |
| **PATCH** (`0.0.X`) | Backward-compatible fixes and polish. | Bug fixes in a skill; clarifying wording that doesn't change behavior; documentation, README, or manifest-metadata corrections. |

### The 0.x phase (current)

While the version is `0.y.z`, the public surface is considered **unstable** and
may change at any time. During this phase:

- **Breaking changes bump MINOR** (`0.y.z` → `0.(y+1).0`).
- **New features and fixes bump PATCH** (`0.y.z` → `0.y.(z+1)`).

Reaching **`1.0.0`** is a deliberate decision that declares the public surface
**stable**. From `1.0.0` on, the standard table above applies and any breaking
change requires a MAJOR bump.

### Pre-releases

For previews, append a hyphen and identifier: `0.2.0-rc.1`, `1.0.0-beta.1`.
Pre-releases sort below their final version and signal "not yet stable".

## Release checklist

1. **Confirm the version.** Decide the bump from the table above based on what
   changed since the last tag (`git log <last-tag>..HEAD`).
2. **Bump the version** in `.claude-plugin/plugin.json` (`version`) and update any
   version string in the READMEs (e.g. the Status & roadmap line).
3. **Commit** the release prep: `chore(release): vX.Y.Z`.
4. **Tag** the release commit with an annotated tag:
   `git tag -a vX.Y.Z -m "Specsmith vX.Y.Z — <title>"`.
5. **Push** the commit and the tag: `git push origin <branch> && git push origin vX.Y.Z`.
6. **Publish the GitHub Release** against the tag, using the title and notes
   template below. These notes are the authoritative record of what changed in
   the release — there is no separate changelog file.

## Release title format

```
Specsmith vX.Y.Z — <Short, human title>
```

Examples:
- `Specsmith v0.1.0 — Initial MVP`
- `Specsmith v0.2.0 — Parametrized git flow`
- `Specsmith v1.0.0 — Stable release`

## Release notes template

Paste this into the GitHub Release body and fill it in. These notes are the
authoritative record of what changed in the release.

```markdown
## Specsmith vX.Y.Z — <title>

<One or two sentences on what this release is and who should care.>

### Added
- ...

### Improved
- ...

### Fixed
- ...

### Upgrading
<Anything users must do to adopt this version. Omit if nothing is required.>

**Full changelog:** https://github.com/murilobauck/specsmith/compare/<prev-tag>...vX.Y.Z
```
