<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 📦 List GitHub Releases

Returns a list of releases for the current repository. Supports text and JSON
output formats, tag checking, and filtering of draft/pre-release entries.
Limited to 1000 records due to GitHub API query limits.

## github-list-releases-action

## Usage Example

Lists repository releases, optionally checking whether a specific tag already
exists as a release.

<!-- markdownlint-disable MD013 -->

```yaml
steps:
  - name: "List GitHub Releases"
    id: list-releases
    uses: lfreleng-actions/github-list-releases-action@main
    with:
      TAG: "v1.0.0"
      SUMMARY_OUTPUT: "true"
```

<!-- markdownlint-enable MD013 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Name            | Required | Default | Description                                    |
| --------------- | -------- | ------- | ---------------------------------------------- |
| TAG             | False    |         | Check if this tag/version already exists       |
| SUMMARY_OUTPUT  | False    | false   | Displays summary output in GitHub step summary |
| PRODUCTION_ONLY | False    | false   | Exclude pre-release and draft releases         |
| RETURN_TYPE     | False    | text    | Output format: text or json                    |
| JSON_FIELDS     | False    | tagName | Fields to return when using JSON return type   |
| ORDER           | False    | desc    | Sort order: asc or desc                        |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Name     | Description                                        |
| -------- | -------------------------------------------------- |
| RELEASES | List of releases in specified output format        |
| RELEASED | Whether the provided tag/version already exists    |

<!-- markdownlint-enable MD013 -->

## Requirements/Dependencies

The GitHub CLI (`gh`) must be available in the runner's PATH. This is
pre-installed on GitHub-hosted runners.

## Notes

- Setting `RETURN_TYPE` to `json` requires the `JSON_FIELDS` input
  (defaults to `tagName`).
- Tag checking supports both prefixed (`v1.0.0`) and unprefixed (`1.0.0`)
  version strings.
