# GitHub Action to Convert PR to Draft

Converts the current (or specified) pull request to a draft

## Usage

### Inputs

- `token`: The GitHub token to allow authenticated actions
- `pull-request-node-id`: The GitHub node id of the pull request to mark as draft

### Example Workflow

```yaml
# Marks all newly opened pull requests as drafts
name: Draft on Open
on:
  pull_request:
    types: [ opened ]

jobs:
  mark-as-draft:
    name: Mark as draft
    if: github.event.pull_request.draft == false
    runs-on: ubuntu-latest
    steps:
      - name: Mark as draft
        uses: voiceflow/draft-pr@latest
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

### Retrieving the Node ID

When calling this action from a workflow triggered by a `pull_request` event, it will automatically apply to the current pull request. If you want to apply this action to a different PR, you can retrieve its node ID by calling the command `gh pr view $PR --json id --jq .id` where `$PR` is the number, url, or branch of your PR.

## License

MIT
