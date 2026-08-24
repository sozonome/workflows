# workflows

### References

- https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Troubleshooting

### update-license workflow

Ensure GITHUB_TOKEN has write access to the repository.
Open Repository settings: "Actions" -> "General" -> "Workflow permissions"

### release workflow

`EBADDEVENGINES Invalid semver version ... does not match ... for "runtime"`

The target repo pins Node via `engines`/`devEngines` (e.g. `devEngines.runtime.version: "24.16.0"`),
but the workflow installed a newer Node. Pass a matching `node-version` input:

```yaml
jobs:
  release:
    uses: agustinusnathaniel/workflows/.github/workflows/release.yml@main
    with:
      node-version: "24.16.0"
```

Alternatively, relax the pin in the target repo's `package.json`
(e.g. `">=24.11 <25"`) so newer Node patches satisfy it.
