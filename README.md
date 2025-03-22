# Comment Branch Name Action

This GitHub Action automatically comments on newly opened issues with a suggested branch name based on your application name and the issue number. It can also be triggered on existing issues by adding a comment containing `:comment-branch`.

## Features

-   Generates a branch name using your application name and the issue number
-   Sanitizes the app name by replacing spaces and special characters
-   Adds a comment to the issue with the branch name and git checkout command
-   Supports triggering on existing issues via `:comment-branch` comment

## Usage

Create a workflow file (e.g., `.github/workflows/issue-branch.yml`) with the following content:

```yaml
name: Comment Branch Name on Issues

on:
    issues:
        types: [opened]
    issue_comment:
        types: [created]

permissions:
    issues: write

jobs:
    comment-branch-name:
        runs-on: ubuntu-latest
        if: ${{ github.event_name == 'issues' || contains(github.event.comment.body, ':comment-branch') }}
        steps:
            - name: Comment Branch Name
              uses: SEKI-YUTA/action-comment-working-branch-name@v1.0.3
              with:
                  app-name: "Your App Name"
```

## Inputs

| Input      | Description                                                       | Required | Default |
| ---------- | ----------------------------------------------------------------- | -------- | ------- |
| `app-name` | The name of your application that will be used in the branch name | Yes      | `app`   |

## Example

When a new issue is opened or when someone comments `:comment-branch` on an existing issue, the action will add a comment like:

```
This issue's work branch is "Your-App-Name-123".
branch name:
```

Your-App-Name-123

```
To checkout this branch, run the following command:
```

git checkout -b Your-App-Name-123

```

## Using with Existing Issues

To generate a branch name for an existing issue, simply add a comment containing the text `:comment-branch` to that issue. The action will automatically detect this and generate the branch name comment.

## License

MIT
```
