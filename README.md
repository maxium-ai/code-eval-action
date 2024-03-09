# code-eval-action

Evaluates the code written as part of a pull request to assess its complexity and provide
a score on the effort required to put it together. It will then leave a comment on the PR
with the response from Maxium's server and delete any previous comments.

## Usage

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
