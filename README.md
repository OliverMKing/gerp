# gerp

GitHub Enforced Repository Patterning

## Usage

First, create a template repository that will house your templates. After, add a `.github/workflows/template_dispatch.yaml` file with the following contents.

```yaml
name: Template dispatch

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  release-pr:
    uses: OliverMKing/gerp/.github/workflows/template_dispatch.yaml@main
```

Create a `.gerp/config.json` file.

```json
{
  "repos": {
    "org/repo": {
      "inputs": {}
    },
    "org2/repo2": {
      "inputs": {}
    }
  }
}
```

The key of each entry in repos is the full repository name (org + name). Inputs are the input object expected by [mustache](https://www.npmjs.com/package/mustache) for templating.

Then create a `template` directory. The inside the template directory represent the root directory of your supported repos. For example, `template/.github/workflows/test.yaml` maps to `.github/workflows/test.yaml` in your supported repos. Mustache expressions can be used inside files in the `template` directory.
