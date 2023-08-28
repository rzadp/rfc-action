# rfc-propose

## Description

A GitHub Action aiming to help in the creation of RFC proposal referenda.

Learn more about the RFC proposal process [here](https://github.com/polkadot-fellows/RFCs#process).

## Usage

To use the action in a repository, add a job that is going to run on specific comments on PRs:

```yaml
name: RFC propose

on:
  issue_comment:
    types: [created]

permissions:
  pull-requests: write

jobs:
  rfc-propose:
    name: Propose an RFC creation transaction
    if: ${{ github.event.issue.pull_request && startsWith(github.event.comment.body, '/rfc-propose') }}
    runs-on: ubuntu-latest
    steps:
      - uses: paritytech/rfc-propose@main
    env:
      GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

### Environment variables

The action uses the `GH_TOKEN` environment variable supplied to it.

The built-in `secrets.GITHUB_TOKEN` can be used, as long as it has the `pull-requests` write permissions.
