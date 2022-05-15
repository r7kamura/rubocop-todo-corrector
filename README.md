# rubocop-todo-corrector

[Custom action](https://docs.github.com/en//actions/creating-actions/about-custom-actions)
to auto-correct [RuboCop](https://github.com/rubocop/rubocop) ToDo offenses and create pull request.

## Usage

An example workflow to run rubocop-todo-corrector via
[manual running](https://docs.github.com/en//actions/managing-workflow-runs/manually-running-a-workflow).

```yaml
# .github/workflows/rubocop-todo-corrector.yml
name: rubocop-todo-corrector

on:
  workflow_dispatch:

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: r7kamura/rubocop-todo-corrector@v0
```

Now you can run rubocop-todo-corrector via GitHub Actions page,
or [GitHub CLI](https://cli.github.com/) like this:

```
gh workflow run rubocop-todo-corrector
```

## Inputs

### `base_branch`

- Pull request base branch.
- default: `"main"`

### `mode`

- Mode to select deletion target.
- default: `"random"`
- Choose from the following options:
  - `"first"`
  - `"last"`
  - `"least_occured"`
  - `"most_occured"`
  - `"random"`
