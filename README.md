# Launchable record build action

# Usage

By default, we suggest using the [record build and test results action](https://github.com/marketplace/actions/record-build-and-test-results-action).

However if your code repository/repositories is/are not available in the step where you run tests, you can split up the two steps (record build and record tests).

Use this action to record a build, then use the [Launchable record tests to build action](https://github.com/marketplace/actions/record-test-results-to-build-action) to record tests.

## Usage with `actions/checkout`

If you use `actions/checkout`, set fetch-depth: 0 as shown in the example below. Without this setting, Launchable will not receive information about all your commits.

```yaml
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
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
The Launchable record build action is licensed under the [Apache license](./LICENSE).
