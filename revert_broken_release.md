# Reverting failed release.

Some instructions for reverting a failed release.

## On develop branch

1. Turn off branch protection on develop. 

2. Use git to revert version bump commit.

3. Push to remote.

4. Turn branch protection on.

5. Delete tag associated with botched release locally: `git tag -d <tag_name>`

6. Delete tag associated with botched release remotely: `git push --delete origin tagname`

7. Revert PR for failed release through GitHub. Make sure to add [skip release]' to PR title to avoid release!


