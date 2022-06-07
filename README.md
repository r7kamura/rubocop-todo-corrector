# rubocop-todo-corrector

[Custom action](https://docs.github.com/en//actions/creating-actions/about-custom-actions)
to auto-correct [RuboCop](https://github.com/rubocop/rubocop) ToDo offenses and create pull request.

## How it works?

![](images/workflow.png)

![](images/pull-request.png)

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

### `cop_name`

- Pass cop name if you want to pick a specific cop.
- optional
- e.g. `Style/NegatedIf`

### `github_token`

- GitHub access token to run another workflows from new pull request.
    - Don't forget to add `workflow` scope to this token
- optional

### `label`

- Pull request label name.
- optional
- e.g. `rubocop-todo-corrector`

### `mode`

- Mode to select deletion target.
- default: `random`
- Choose from the following options:
  - `"first"`
  - `"last"`
  - `"least_occurred"`
  - `"most_occurred"`
  - `"random"`

### `only_safe`

- Exclude unsafe cops.
- default: `true`
