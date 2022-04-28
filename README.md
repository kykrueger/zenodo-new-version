# zenodo-new-version
Connect a zenodo deposition to your github repo with the 'zenodo-new-version' GitHub action.
Use this action only after you have already created a deposition.

This action:
1. Creates a new version of a Deposition given an ID of a prior version.
1. Replaces the prior DOI where it is found in the documents listed in a `.whitelist_replace_doi` file.

Be sure to chain this action with an upload, commit, tag and release action.
