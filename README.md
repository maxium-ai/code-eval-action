# Maxium Code Eval Action

Evaluates the code written as part of a pull request to assess its complexity and provide
a score on the effort required to put it together. It will then leave a comment on the PR
with the response from Maxium's server and delete any previous comments from the same action.

## Usage

To integrate Maxium with your Actions pipeline, specify the name of this repository with a tag number / branch (`@v1.0.0-beta.1` is recommended) as a `step` within your `workflow.yml` file.

This Action also requires you to provide a Maxium API key which you can get by signing up [here](https://www.maxium.ai/#contact).
(tip: in order to avoid exposing your token, [store it](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions) as a `secret`).

Inside your `.github/workflows/workflow.yml` file:

```yaml

name: Maxium Code Eval

on:
  pull_request:
    types:
      - opened
      - synchronizd

jobs:
  code-eval:
    runs-on: self-hosted
      timeout-minutes: 5
    steps:
      - name: Maxium Code Eval Action
        uses: maxium-ai/code-eval-action@master
        with:
          github-token: "${{ secrets.GITHUB_TOKEN }}"
          maxium-ai-api-key: "${{ secrets.MAXIUM_AI_API_KEY }}"

```

> [!NOTE]
> This assumes that you've added your Maxium API key inside *Settings > Secrets* as `MAXIUM_AI_API_KEY`.

## Arguments

Maxium's Code Eval Action supports the `v1/code-eval/pull-request` endpoint. The endpoint takes the following inputs as part of the request body to evaluate code changes:

| Input  | Description | Required |
| :---       |     :---     |    :---:   |
| `X-API-Key` | Maxium's API key. Used to authorize code evals | Required 
| `github_author_id` | Specify the github author id of the pull request | Required 
| `github_username` | Specify the github username of the author of the pull request | Required
| `pull_request_id` | Specify the github assigned pull request id | Required 
| `commit_id` | The commit hash of the code changes to be evaluated | Required 
| `diff` | The code changes in diff format associated with the pull request | Required 
| `branch_name` | The github branch name on which changes are being pushed | Required 
| `github_repository` | Github repository name that contains the pull request | Required 
| `github_repository_id` | Github assigned repository id for the repo that contains the pull request | Required 
| `labels` | List of labels assigned to pull request at the time of workflow initiation | Optional 
