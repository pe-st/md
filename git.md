git notes
=========

## information commands

- git config -l
- git status
- git remote [-v]

- git log
  git log --pretty=format:"%h %s" --graph
  With author date and name
  git log --pretty=format:"%h %ai %an: %s" --all
  With complete hash and the internal date format
  git log --pretty=format:"%H %ad %ai %an: %s" --date=raw --all

- git diff HEAD

  The HEAD is a pointer that holds your position within all your different commits.
  By default HEAD points to your most recent commit, so it can be used as a quick
  way to reference that commit without having to look up the SHA.

- `git branch` or `git branch --all`
- `git remote` or `git remote -v`

- `git show-ref`


## repositories

- new repo: `git init`
- initial download repo: `git clone <URL>`
- get, don't merge: `git fetch`
- get and merge: `git pull` or `git pull origin master`
- upload: `git push` or `git push -u origin master`
  The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do

### import local repo in GitHub

git clone --bare --no-hardlinks file:///Users/pesche/Documents/dev/git/gugus/emacs.d
cd emacs.d.git
git push --mirror https://github.com/pe-st/dot-e.git

### clone into existing directory

Clone into new directory, mv the .git folder


### remotes

- 

## files

- 'stage' a file for commit: `git add <file>`
- unstage a file: `git reset <file>`
- revert a file to the state of the last commit: `git checkout -- <file>`
  (`--` to protect from changing to a branch called `<file>`)
- remove a file from the repo (a branch): `git rm <file>`
- commit what is staged: `git commit -m "comment"`
- update last commit with stage: `git commit --amend`


## branches

- create a new branch: `git branch <branchname>`
- switch to a branch: `git checkout <branchname>`
- combine creation/switch: `git checkout -b <branchname>`
- merge a branch into the current branch: `git merge <branchname>`
- delete a branch: `git branch -d <branchname>`
  (if there are unmerged changes: `git branch --force -d <branchname>`)

### under the hood

Branches are stored in .git/refs

- master is in .git/refs/heads/master
- local branches are in .git/refs/heads/<localbranch>
- remote branches are in .git/refs/remotes, e.g. .git/refs/remotes/origin/trunk
- local branch from remote branch (tracking branch): `git checkout -b b42 origin/b42`
  or `git checkout --track origin/b42`
- delete a remote branch: `git push origin :<branch>`


### merge

- fast forward: current branch had no modifications after the branching point


### remote repo

- `git remote add origin <URL>`

  Git doesn't care what you name your remotes, but it's typical to name your main one `origin`.


## stash




## SVN

cloning of fo_java since the creation of the ao directory (SVN 29714)

### svn config for fo_test

Versuch:

    set SVN_REPO_FO_TEST=(as in wiki)
    git svn init --username=tksnp --prefix=origin/ --ignore-paths="^(?:AFO|static_files)" %SVN_REPO_FO_TEST% fo_test

corresponding line in .git/config:

```
[svn-remote "svn"]
	ignore-paths = ^(?:AFO|static_files) 
```

change these to .git/config:

```
[svn-remote "svn"]
	...
	fetch = trunk:refs/remotes/origin/trunk
	fetch = ao:refs/remotes/origin/ao
	branches = branches/{EmacsNsk,AtmaTester}/*:refs/remotes/origin/branches/*
	tags = tags/*:refs/remotes/origin/tags/*
```

git svn fetch --username=tksnp -A../authors >> ../fo_test_fetch.txt

takes about 45 minutes for 733 revisions

### svn config for fo_java

two repos: ao and trunk

#### fo_java_trunk

```
set SVN_REPO_FO_JAVA=(as in wiki)
git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA% fo_java_trunk

[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
	include-paths = /cdfa.(?:business|test|utils)/
	fetch = trunk:refs/remotes/origin/trunk

cd fo_java_trunk

git svn fetch --username=tksnp -A../authors >> ../fo_java_fetch.txt 2>&1

(ca 2000-3000 revisions/h)

(ca r18300 2014-06-30 18:00, r19100 18:42 : 1200/h)
(ca r19100 2014-07-02 08:52, r21200 10:29 : 1200/h)
(ca r21200 2014-07-02 11:11, r27000 16:16)
(ca r27900 2014-07-02 18:11, r36100 21:14 : 2700/h)
```


#### fo_java_ao

   git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA% fo_java_ao

```
[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
	url = ...
	fetch = ao:refs/remotes/origin/ao
```

First fetch

    cd fo_java_ao
    git svn fetch --username=tksnp -A../authors -r29714:HEAD  > ../fo_ao_fetch.txt 2>&1

Subsequent fetches

    git svn fetch --username=tksnp -A../authors >> ../fo_ao_fetch.txt 2>&1


#### fo_java_ao1

```
git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA% fo_java_ao1

[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
	url = ...
	fetch = ao:refs/remotes/origin/ao/trunk
	branches = ao/*/branches:refs/remotes/ao/branches/*
	tags = ao/*/tags:refs/remotes/ao/tags/*

cd fo_java_ao1

git svn fetch --username=tksnp -A../authors -r29714:HEAD  > ../fo_ao1_fetch.txt 2>&1

git svn fetch --username=tksnp -A../authors >> ../fo_ao1_fetch.txt 2>&1

(ca r29714 2014-07-04 16:18, r32217 17:46 : 2500 in 90 min, ~1600/h)
(   r32218 2014-07-06 11:36, r39016 22:06 : 6800 in 630 min, ~650/h über langsame Leitung)
```


#### scratch

```
[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
#	fetch = ao:refs/remotes/origin/ao
# wildcards don't work with fetch
#	fetch = ao/*/trunk:refs/remotes/origin/ao/trunk/*
	fetch = ao/root/trunk:refs/remotes/origin/ao/root
	fetch = ao/common/configuration/trunk:refs/remotes/origin/ao/common/configuration
	fetch = ao/common/connector/trunk:refs/remotes/origin/ao/common/connector
	fetch = ao/common/core/trunk:refs/remotes/origin/ao/common/core
	fetch = ao/common/ddl/trunk:refs/remotes/origin/ao/common/ddl
	fetch = ao/common/ee/trunk:refs/remotes/origin/ao/common/ee
	fetch = ao/common/services/test/trunk:refs/remotes/origin/ao/common/services/test
	fetch = ao/common/services/nsb/trunk:refs/remotes/origin/ao/common/services/nsb
	fetch = ao/common/services/rc/trunk:refs/remotes/origin/ao/common/services/rc
	fetch = ao/common/services/test-ear/trunk:refs/remotes/origin/ao/common/services/test-ear
	fetch = ao/common/services/services-ear/trunk:refs/remotes/origin/ao/common/services/services-ear
	fetch = ao/common/services/cardrecognition/trunk:refs/remotes/origin/ao/common/services/cardrecognition
	fetch = ao/common/services/businesslogger/trunk:refs/remotes/origin/ao/common/services/businesslogger
	fetch = ao/common/services/cardsegment/trunk:refs/remotes/origin/ao/common/services/cardsegment
	fetch = ao/common/services/dccs/trunk:refs/remotes/origin/ao/common/services/dccs
	fetch = ao/common/test/trunk:refs/remotes/origin/ao/common/test
	fetch = ao/common/utils/trunk:refs/remotes/origin/ao/common/utils
	fetch = ao/ifo/itx/itx-api/trunk:refs/remotes/origin/ao/ifo/itx/itx-api
	fetch = ao/ifo/itx/itx-legacy/trunk:refs/remotes/origin/ao/ifo/itx/itx-legacy
	fetch = ao/ifo/itx/itx-mock/trunk:refs/remotes/origin/ao/ifo/itx/itx-mock
	fetch = ao/tfo/atm/trunk:refs/remotes/origin/ao/tfo/atm
# not sure if this works
#	branches = ao/*/branches:refs/remotes/ao/branches/*
#	tags = ao/*/tags:refs/remotes/ao/tags/*
```

### errors with git svn

- not a valid SHA1

  went away when importing without -r switch, see
  http://stackoverflow.com/a/23525321/3686
  You didn't fetch from revision old enough to span at least one commit into trunk (for example, using -r option).

- RA layer request failed: [...]
  Could not read chunk size: Connection reset by peer [...] at /usr/lib/perl5/site_perl/Git/SVN/Ra.pm line 290

  Fetching one big commit (r284?), took too long from home (slower connection), but worked in the office

- RA layer request failed: REPORT request failed on '/svn/cdfa/fo_java/!svn/vcc/default':
  REPORT of '/svn/cdfa/fo_java/!svn/vcc/default': Could not read response body:
  Secure connection truncated (https://vmzdtooldev02.telekurs.com) at /usr/lib/perl5/site_perl/Git/SVN/Ra.pm line 290

- RA layer request failed: PROPFIND request failed on '/svn/cdfa/fo_java': PROPFIND of '/svn/cdfa/fo_java':
  could not connect to server (https://...) at /usr/lib/perl5/site_perl/Git/SVN/Ra.pm line 290
  (network cable pulled)


<!--
Local Variables:
coding: utf-8
End:
-->
