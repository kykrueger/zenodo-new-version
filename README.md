# zenodo-new-version
Connect a zenodo deposition to your github repo with the 'zenodo-new-version' GitHub action.
Use this action only after you have already created a deposition.

This action:
1. Creates a new version of a Deposition given an ID of a prior version.
1. Replaces the prior DOI with the newly prereserved one in the documents found in the provided whitelist file; `whitelist_replace_doi` defaults to `.zenodo_whitelist_replace_doi`.

Be sure to chain this action with an upload and commit. The following example runs whenever a txt md or csv file are changed:

``` yaml
name: Basic Workflow

on:
  push:
    branches: [ main ]
    paths:
      - '**.txt'
      - '**.md'
      - '**.csv'
  workflow_dispatch:
env:
  zenodo_deposition_id: <YOUR DEPSITION ID HERE>
  zenodo_server: 'https://sandbox.zenodo.org'
jobs:
  new_version:
    name: Create new version of zenodo deposition
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: kykrueger/zenodo-new-version@v1.0.1
        with:
          zenodo_deposition_id: ${{ env.zenodo_deposition_id }}
          zenodo_server: ${{ env.zenodo_server }}
          zenodo_token: ${{ secrets.ZENODO_SANDBOX_TOKEN }}
      - uses: kykrueger/zenodo-publish@v1
        with:
          zenodo_deposition_id: ${{ env.zenodo_deposition_id }}
          zenodo_server: ${{ env.zenodo_server }}
          zenodo_token: ${{ secrets.ZENODO_SANDBOX_TOKEN }}
      - uses: EndBug/add-and-commit@v7.1.1
        with:
          message: 'published to Zenodo'
```
