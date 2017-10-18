 - github development workflow
   - http://scottchacon.com/2011/08/31/github-flow.html
   - http://nvie.com/posts/a-successful-git-branching-model/
 - working on pull request branches opened from forks, without adding the fork as a remote (copied from[this post](https://github.com/obspy/obspy/pull/1756#issuecomment-337398126)):

```
Strictly speaking, you do not need another remote. To just download the code
use `git fetch upstream pull/1756/head:fix_arclink`. To push, you can specify
the remote url without adding it `git push git@github.com:petrr/obspy fix_arclink`.

I also like to set an `insteadOf` config like:

"""
$ git config --list | grep instead
url.git://github.com/.insteadof=github:
url.git@github.com:.pushinsteadof=github:
"""

so that I can do `git push github:petrr/obspy fix_arclink`.
```

 - convert existing issue into a pull request
   - can be done using [github/hub](https://github.com/github/hub)
```bash
hub pull-request -i 1704 -b obspy:master -h obspy:trace_always_contiguous
```
   - or via a simple POST command, e.g. using `curl`:
```bash
curl --user megies --request POST --data '{"issue": "2", "head": "megies:testbranch2", "base": "master"}' https://api.github.com/repos/obspy/obspy/pulls
# in case of 2-factor authentication enabled..
curl --header "X-GitHub-OTP: 123456" --user megies --request POST --data '{"issue": "2", "head": "megies:testbranch2", "base": "master"}' https://api.github.com/repos/obspy/obspy/pulls
```
      - **issue**: number of the *already existing* normal issue
      - **head**: *repository/branch* that should be pulled in
      - **base**: branch that the pull request should be merged into (target repository specified in the url), usually either `master` (for feature branches) or `releases` (for bug fixes)
 - interaction with svn
   - https://github.com/blog/1178-collaborating-on-github-with-subversion
 - Squash commits [using `git rebase`](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html)
```
# squash the last 4 commits interactively
# Only do this on a branch no one else is using
git rebase -i HEAD~4
git push --force upstream my_feature_branch
```