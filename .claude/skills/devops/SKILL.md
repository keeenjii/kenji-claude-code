---
name: devops
description: Interact with Azure Devops. Use when asked to do things related to devops.
---

Interact with Azure DevOps. Examples:

- Create a pull request for the current branch using curl and the Azure DevOps API.

- Add comments to PRs

- Read work items

## General

IMPORTANT: Always disclose AS TEXT IN THE CONTENT that you are the one creating the PRs, comments etc.

Load the env vars by running:

```bash
eval "$(grep '^AZURE_DEVOPS_' ~/Documents/epoch/Epoch/services/webserver/.env)"
```

Run curl commands directly and read the JSON output yourself - don't pipe to Python for parsing.

If the user provides arguments like `$ARGUMENTS`, use them accordingly.

If the user mentions tests that have been performed (e.g., "tested login" or "verified routing works"), check the corresponding checkboxes in the template by changing `- [ ]` to `- [x]` for those items.

Only include a clipboard image if the user explicitly mentions it. When including an image, place it BEFORE the "Manual Testing Checklist" section.

To upload a clipboard image, use a Python one-liner to get the image bytes and pipe to curl:

```bash
python3 -c "from PIL import ImageGrab; import sys; img=ImageGrab.grabclipboard(); img and img.save(sys.stdout.buffer, 'PNG')" | \
curl -s -X POST "https://dev.azure.com/$AZURE_DEVOPS_ORG/$AZURE_DEVOPS_PROJECT/_apis/wit/attachments?fileName=screenshot.png&api-version=7.0" \
  -H "Content-Type: application/octet-stream" \
  -H "Authorization: Basic $(echo -n ":$AZURE_DEVOPS_PAT" | base64)" \
  --data-binary @-
```

To create the PR (use $AZURE_DEVOPS_TEAM_ID for the Epoch Team reviewer):

```bash
curl -s -X POST "https://dev.azure.com/$AZURE_DEVOPS_ORG/$AZURE_DEVOPS_PROJECT/_apis/git/repositories/$AZURE_DEVOPS_REPO/pullrequests?api-version=7.0" \
  -H "Content-Type: application/json" \
  -H "Authorization: Basic $(echo -n ":$AZURE_DEVOPS_PAT" | base64)" \
  -d '{
    "sourceRefName": "refs/heads/BRANCH_NAME",
    "targetRefName": "refs/heads/master",
    "title": "PR_TITLE",
    "description": "PR_DESCRIPTION",
    "reviewers": [{"id": "$AZURE_DEVOPS_TEAM_ID"}]
  }'
```

## Creating Pull Requests

IMPORTANT: Always include the PR template from `~/Documents/epoch/Epoch/.azuredevops/pull_request_template.md` as the description.

Read the template file first. Replace `<insert description here>` with a summary of the changes based on the commits in the branch.

If not instructed otherwise, add "Epoch Team" as required reviewer.

IMPORTANT: When using jq to build JSON for PR descriptions containing markdown images, jq's `-Rs` flag will escape exclamation marks with backslashes, breaking image syntax. To avoid this, either:

- Don't use jq for descriptions with images - use heredoc or direct JSON construction instead

- Or post-process the jq output to unescape exclamation marks with sed

## Commenting

PR comment types: 0=unknown, 1=text, 2=codeChange, 3=system. Use 1 for regular comments.

When commenting about specific parts of the code, put the comment in the code rather than a generic comment.

Use markdown formatting in PR descriptions and comments (headers, lists, code blocks, etc.).

Before creating a new comment, check the current conversations if the subject is already being discussed and if so put the comment there.

After commenting, make sure to follow up with appropriate action (Approve, Approve with suggestions, wait for author, reject).
