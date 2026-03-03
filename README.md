# major-tag-floater

Automated floating major version tag updater for semantic versioning.

This GitHub Action updates the floating major version tag (e.g. `v1`) to always point to the latest release commit, following the convention used by many popular GitHub Actions.

## Usage

Add the following workflow to your repository (e.g. `.github/workflows/release-tag.yml`):

```yaml
name: Update major version tag

on:
  release:
    types:
      - published

jobs:
  tag:
    runs-on: ubuntu-latest
    if: "!github.event.release.prerelease"
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      - uses: kotaoue/major-tag-floater@v1
```

## Inputs

| Name  | Description                                                                 | Required | Default                              |
|-------|-----------------------------------------------------------------------------|----------|--------------------------------------|
| `tag` | The full release tag (e.g. `v1.2.3`). Defaults to the tag from the release event. | No | `${{ github.event.release.tag_name }}` |

## How it works

When a release is published, this action:

1. Extracts the major version prefix from the release tag (e.g. `v1` from `v1.2.3`).
2. Force-updates the major version tag to point to the current commit.
3. Force-pushes the updated tag to the repository.

## License

[MIT](LICENSE)
