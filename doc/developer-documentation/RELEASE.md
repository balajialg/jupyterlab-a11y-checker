# Release & Deployment

This doc is about how `jupyterlab-a11y-checker` is versioned and published.

Releases are automated through a single GitHub Actions workflow
(`.github/workflows/publish.yml`) using
[release-please](https://github.com/googleapis/release-please) + OIDC Trusted
Publishing (no stored tokens). Two packages are published:

| Package              | Registry | Tag prefix     | Name                           |
| -------------------- | -------- | -------------- | ------------------------------ |
| `packages/extension` | PyPI     | `extension-v*` | `jupyterlab-a11y-checker`      |
| `packages/cli`       | npm      | `cli-v*`       | `@jupyterlab-a11y-checker/cli` |

(`packages/core` is bundled into both; it is not published on its own.)

## Cutting a release

1. **Make your change** on a branch and commit it with a **Conventional Commit**
   message (e.g. `fix: handle empty alt text` or `feat: add severity column`).
   See [Versioning](#versioning) for how the prefix maps to the version bump.
2. **Open a PR and merge it into `main`.**
3. On the push to `main`, release-please opens (or updates) a **release PR**
   titled `chore: release <package> v<version>`.
4. **Review the release PR** — check the proposed version bump and the generated
   `CHANGELOG`.
5. **Merge the release PR.** This tags the commit (`extension-v…` / `cli-v…`),
   creates the GitHub Release, and the workflow automatically publishes the
   package to PyPI / npm with provenance.

## Versioning

The version is derived from commit prefixes since the last release — you never
type a version number:

| Prefix                                         | Bump  |
| ---------------------------------------------- | ----- |
| `fix:`                                         | patch |
| `feat:`                                        | minor |
| `feat!:` / `BREAKING CHANGE:`                  | major |
| `chore:`, `docs:`, `refactor:`, `test:`, `ci:` | none  |

- No release PR appears until a `feat:` or `fix:` lands for that package
  (chore/docs/etc. alone won't trigger one).
- A commit only affects a package if it changes files under that package's
  directory (`packages/extension/` or `packages/cli/`).

## Manual / retry publish

If a publish fails for a transient reason (the release and tag already exist),
re-run just the publish — no new release needed:

```bash
gh workflow run publish.yml -f target=cli         # republish the CLI to npm
gh workflow run publish.yml -f target=extension   # republish the extension to PyPI
```

Retries can't double-publish (PyPI uses `skip-existing`; npm rejects an existing
version).
