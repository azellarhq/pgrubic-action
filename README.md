# pgrubic-action

[![pgrubic-action](https://img.shields.io/badge/pgrubic-action-purple.svg)](https://github.com/azellarhq/pgrubic-action/)
[![Version](https://img.shields.io/github/v/release/azellarhq/pgrubic-action?label=version)](https://github.com/marketplace/actions/pgrubic-action)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
[![CI](https://github.com/azellarhq/pgrubic-action/actions/workflows/ci.yml/badge.svg)](https://github.com/azellarhq/pgrubic-action/actions/workflows/ci.yml)
[![release](https://github.com/azellarhq/pgrubic-action/actions/workflows/release.yml/badge.svg)](https://github.com/azellarhq/pgrubic-action/actions/workflows/release.yml)

A GitHub Action to run [**pgrubic**](https://bolajiwahab.github.io/pgrubic), a PostgreSQL linter and formatter for schema migrations and design best practices.

This action runs `pgrubic lint --generate-lint-report` by default, but it can do
anything `pgrubic` can.

## Commenting on pull requests

This action, by default, comments with lint reports on pull requests on `pull_request` events and therefore requires the necessary permissions for publishing new comments in pull requests.

```yaml
permissions:
  # Gives the action the necessary permissions for publishing new
  # comments in pull requests.
  pull-requests: write
```

## Inputs

| Input             | Description                                                                                                            | Default            |
|-------------------|------------------------------------------------------------------------------------------------------------------------|--------------------|
| `args`            | The arguments to pass to the **pgrubic** command. See [Running pgrubic](https://bolajiwahab.github.io/pgrubic/cli).    | `lint --generate-lint-report`             |
| `pgrubic-version` | The version of **pgrubic** to use, e.g., `0.9.0`.                                                                      | `latest`           |
| `src`             | The directory or files to run **pgrubic** on.                                                                          | [github.workspace](https://docs.github.com/en/actions/reference/contexts-reference#github-context:~:text=the%20workflow%20file.-,github.workspace,-string)                                 |

## Outputs

| Output                      | Description                                 |
|-----------------------------|---------------------------------------------|
| `installed-pgrubic-version` | The version of the installed **pgrubic**.   |

## Usage

### Basic

```yaml
- uses: azellarhq/pgrubic-action@v2
```

### Specifying a different source directory

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    src: "./src"
```

### Specifying multiple files

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    src: >-
      path/to/file1.sql
      path/to/file2.sql
```

### Specifying multiple directories

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    src: >-
      path/to/dir1
      path/to/dir2
```

### Specifying multiple files and directories

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    src: >-
      path/to/file1.sql
      path/to/file2.sql
      path/to/dir1
      path/to/dir2
```

### To install pgrubic

This action adds **pgrubic** to the PATH, so you can use it in subsequent steps.

```yaml
- uses: azellarhq/pgrubic-action@v2
- run: pgrubic lint
- run: pgrubic format
```

By default, this action runs `pgrubic lint` after installation. If you do not want to run any `pgrubic` command but only install it,
you can use the `args` input to overwrite the default option (`lint`):

```yaml
- name: Install pgrubic without running lint or format
  uses: azellarhq/pgrubic-action@v2
  with:
    args: "--version"
```

### Use `pgrubic format`

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    args: "format --check --diff"
```

### Install a specific version of pgrubic

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    pgrubic-version: "0.6.0"
```

### Install the latest version of pgrubic

```yaml
- uses: azellarhq/pgrubic-action@v2
  with:
    pgrubic-version: "latest"
```

## Contributing

We welcome and greatly appreciate contributions. If you would like to contribute, please see the [contributing guidelines](contributing.md).

## Support

Encountering issues? Take a look at the existing GitHub [issues](https://github.com/azellarhq/pgrubic-action/issues), and don't hesitate to open a new one.

## License

MIT license.
