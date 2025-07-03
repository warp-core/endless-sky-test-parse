# endless-sky-test-parse
An Action to test parse data for https://github.com/endless-sky/endless-sky

## Usage

```yaml
- uses: warp-core/endless-sky-test-parse@master
  with:
    # The repository to test parse. Usually a plugin for Endless Sky.
    # Default: ${{ github.repository }}
    repository:
	# Whether or not to test assets (images and sounds) in addition to data files.
	# Default: false
	parse-assets:
    # The token to use to checkout the repository.
    # Default: ${{ github.token }}
    token:
```

## Example

```yaml
name: CI

on:
  push:
    branches:
      - master
  pull_request:
    types: [opened, synchronize]

concurrency:
  group: ${{ github.ref }}-${{ github.workflow }}-${{ github.event_name }}
  cancel-in-progress: true

jobs:
  test-parse-world-forge:
    name: Data Files
    runs-on: windows-2022
    steps:
    - uses: warp-core/endless-sky-test-parse@master
      with:
        repository: EndlessSkyCommunity/world-forge
```

If this action is running within the repository to test parse, no parameters are necessary:

```yaml
    steps:
    - uses: warp-core/endless-sky-test-parse@master
```
