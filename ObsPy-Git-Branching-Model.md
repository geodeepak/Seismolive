This is a sketch of the git branching model for ObsPy. A pdf version can be obtained [here](https://raw.github.com/wiki/obspy/obspy/images/obspy_dev_model.pdf).

The important point is that adding new features and changing existing features has to be kept separate from pure bugfixes. This is necessary to be able to maintain the current stable version with bugfixes (and eventual bug fix releases) without mixing in feature changes. Changed features are only merged into the release branch when a new feature release is made.

This means that the tip of the current maintenance branch (e.g. "maintenance\_1.0.x") will always reflect the behavior of the last feature release (in this case version "1.0.0") plus additional bug fixes since the last release. The tip of the "master" branch will incorporate *both* bugfixes since the last feature release *plus* eventual new features and/or feature changes.

### Branching model
[[images/obspy_dev_model.png]]


### Roadmap for a bugfix:
 - make new branch "fix\_..." starting at the current maintenance branch (e.g. **"maintenance_1.0.x"**), e.g.
```bash
$ git checkout -b fix_some_issue upstream/maintenance_1.0.x
```
 - commit changes and push to obspy/obspy (alias "upstream" in the example) or your own fork
```bash
$ git push --set-upstream upstream fix_some_issue
```
 - open a pull request, **select "obspy:maintenance_1.0.x" as base branch**
 - once pull request is merged into "obspy:maintenance_1.0.x", we will merge "obspy:maintenance_1.0.x" into "obspy:master"
 - optionally: make new tag (e.g. 1.0.2) at the tip of "obspy:maintenance_1.0.x" for a **new minor (bugfix) release**

### Roadmap for a feature change:
 - make new branch "some_name" starting at **"master"**
 - commit changes and push to obspy/obspy or a fork
 - open a pull request, **select "obspy:master" as base branch**
 - optionally: if master branch gets updated with bugfixes from releases branch, occasionally rebase feature branch on current master branch and force-push (or merge master branch into feature branch)
 - optionally: make new tag (e.g. 1.2.0) at the tip of "obspy:master" for a **new major release**
