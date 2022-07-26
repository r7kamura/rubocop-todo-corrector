# rubocop-todo-corrector

[Custom action](https://docs.github.com/en//actions/creating-actions/about-custom-actions) to create a pull request that autocorrects offenses in .rubocop_todo.yml per cop.

## Usage

### Manual running

Add the following workflow file to manually run the action:

```yaml
# .github/workflows/rubocop-todo-corrector.yml
name: rubocop-todo-corrector

on:
  workflow_dispatch:
    inputs:
      cop_name:
        description: Pass cop name if you want to pick a specific cop.
        required: false
        type: string
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: r7kamura/rubocop-todo-corrector@v0
```

Now you can run it via actions page:

![](images/workflow.png)

or if you want to do it from CLI, use [GitHub CLI](https://cli.github.com/) like this:

```
gh workflow run rubocop-todo-corrector
```

After the action is complete, a pull request is created as follows:

![](images/pull-request.png)

### Automatic running

By adding `on.pull_request` to the workflow, you can automatically run it when all other labeled pull requests are merged or closed.

```yaml
# .github/workflows/rubocop-todo-corrector.yml
name: rubocop-todo-corrector

on:
  pull_request:
    types:
      - closed
  workflow_dispatch:
    inputs:
      cop_name:
        description: Pass cop name if you want to pick a specific cop.
        required: false
        type: string

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: r7kamura/rubocop-todo-corrector@feature/infinity
        with:
          cop_name: ${{ github.event.inputs.cop_name }}
          label: rubocop-todo-corrector
```

Note that the `label` input is required to use this feature.
Don't forget to create the label on your repository before you run the action.

## Inputs

### `cop_name`

- Pass cop name if you want to pick a specific cop.
- optional
- e.g. `Style/NegatedIf`

### `github_token`

- GitHub access token for GitHub API calls.
- optional
    - Not required, but if you want to run another workflows from new pull request, you need to pass this token with `workflow` scope.

### `label`

- Pull request label name.
- optional
- e.g. `rubocop-todo-corrector`
- Note: You need to create a label with this name on your repository.

### `mode`

- Mode to select autocorrected cop.
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

## .rubocop_todo_corrector_ignore

You can ignore specific cops by adding a file named `.rubocop_todo_corrector_ignore` to your repository.

See the following page for more details:

- https://github.com/r7kamura/rubocop_todo_corrector#rubocop_todo_corrector_ignore
