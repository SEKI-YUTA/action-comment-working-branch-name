# Comment Branch Name Action

This GitHub Action automatically comments on newly opened issues with a suggested branch name based on your application name and the issue number.

## Features

-   Generates a branch name using your application name and the issue number
-   Sanitizes the app name by replacing spaces and special characters
-   Adds a comment to the issue with the branch name and git checkout command

## Usage

Create a workflow file (e.g., `.github/workflows/issue-branch.yml`) with the following content:

```yaml
name: Comment Branch Name on Issues

on:
    issues:
        types: [opened]

permissions:
    issues: write

jobs:
    comment-branch-name:
        runs-on: ubuntu-latest
        steps:
            - name: Comment Branch Name
              uses: your-username/comment-branch-name@v1
              with:
                  app-name: "Your App Name"
```

## Inputs

| Input      | Description                                                       | Required | Default |
| ---------- | ----------------------------------------------------------------- | -------- | ------- | --- |
| `app-name` | The name of your application that will be used in the branch name | Yes      | `app`   |     |

## Example

When a new issue is opened, the action will add a comment like:

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

```

## License

MIT
