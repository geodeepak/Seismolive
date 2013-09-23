This is a sketch of the git branching model for ObsPy. A pdf version can be obtained [here](https://raw.github.com/wiki/obspy/obspy/images/obspy_dev_model.pdf).

The important point is that adding new features and changing existing features has to be kept separate from pure bugfixes. This is necessary to be able to maintain the current stable version with bugfixes (and eventual bug fix releases) without mixing in feature changes. Changed features are only merged into the release branch when a new feature release is made.

This means that the tip of "releases" branch will always reflect the behavior of the last stable release plus additional bug fixes since the last release. The tip of the "master" branch will incorporate *both* bugfixes since the last stable release *plus* eventual new features or feature changes.

### Branching model
[[images/obspy_dev_model.png]]


### Roadmap for a bugfix:
 - make new branch "fix_..." starting at **"releases"**, e.g.
```bash
$ git checkout -b fix_some_issue upstream/releases
```
 - commit changes and push to obspy/obspy (alias "upstream" in the example) or a fork
```bash
$ git push -u upstream fix_some_issue
```
 - open a pull request, **select "obspy:releases" as base branch**
 - once pull request is merged into "obspy:releases" merge "obspy:releases" into "obspy:master"
 - optionally: make new tag 0.8.x at the tip of "obspy:releases" for a **new minor (bugfix) release**

### Roadmap for a feature change:
 - make new branch "some_name" starting at **"master"**
 - commit changes and push to obspy/obspy or a fork
 - open a pull request, **select "obspy:master" as base branch**
 - optionally: if master branch gets updated with bugfixes from releases branch, occasionally merge master branch into feature branch
 - optionally: make new tag 0.x.0 at the tip of "obspy:master" for a **new major release**