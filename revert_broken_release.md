# Reverting failed release.

Some instructions for reverting a failed release. Only revert if failure occurs before releasing on PyPI. If failure
occurs after PyPI release, merge fixes but don't revert version bump commits.


## On develop branch

1. Turn off branch protection on develop. 

2. Use git to revert version bump commit.

3. Push to remote.

4. Turn branch protection on.

5. Delete tag associated with botched release locally: `git tag -d <tag_name>`

6. Delete tag associated with botched release remotely: `git push --delete origin tagname`

7. Make commits to feature branch to fix problem.

8. Create new pull request to make changes.

9. Turn back on branch protection on develop.

## Current problems

If released to PyPI, can't have release with the same version number.

