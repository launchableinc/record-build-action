# Launchable record build action

# Usage

By default, we suggest using the [record build and test results action](https://github.com/marketplace/actions/record-build-and-test-results-action).

However if your code repository/repositories is/are not available in the step where you run tests, you can split up the two steps (record build and record tests).

Use this action to record a build, then use the Launchable record tests action to record tests.

```yaml
name: Test

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  LAUNCHABLE_DEBUG: 1
  LAUNCHABLE_REPORT_ERROR: 1
  LAUNCHABLE_TOKEN: ${{ secrets.LAUNCHABLE_TOKEN }}

jobs:
  tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Record build action
        uses: launchableinc/record-build-action@v1.0.0
        with:
          build_name: $GITHUB_RUN_ID
      - name: Test
        run: <YOUR TEST COMMAND HERE>
```

## Example

Refer to [go-test example](./.github/workflows/go-test-example.yaml) for example use of the action.

# Inputs

## Required

### `build_name`

[Build](https://docs.launchableinc.com/concepts/build) name that you can give to the current software. You'll use this value when you record tests later, so the value you choose needs to be available in that later step. See [Choosing a value for \<BUILD NAME>
](https://www.launchableinc.com/docs/sending-data-to-launchable/using-the-launchable-cli/recording-builds-with-the-launchable-cli/choosing-a-value-for-build-name/).

## Optional

### `source_path`

Path to a local Git repository/workspace. Default `.`.

### `max_days`

The maximum number of days to collect commits retroactively. Default `30`.

### `no_submodules`

Flag to stop collecting build information from Git Submodules. Default `false`, which means the submodules are collected.

### `python_version`

Python version for the Launchable CLI to use. Default is `3.10`. Change this if your workflow requires a specific Python version.

# License
Launchable data collection actions are licensed under the [Apache license](./LICENSE).
