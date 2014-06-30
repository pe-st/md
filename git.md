git notes
=========

## information commands

- git config -l
- git status
- git remote [-v]

- git log
  git log --pretty=format:"%h %s" --graph
  git log --pretty=format:"%h %ai %an: %s" --all
- git diff HEAD

  The HEAD is a pointer that holds your position within all your different commits.
  By default HEAD points to your most recent commit, so it can be used as a quick
  way to reference that commit without having to look up the SHA.

- `git branch` or `git branch --all`
- `git remote` or `git remote -v`


## repositories

- new repo: `git init`
- initial download repo: `git clone <URL>`
- get, don't merge: `git fetch`
- get and merge: `git pull` or `git pull origin master`
- upload: `git push` or `git push -u origin master`
  The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do

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

...

cd c:\Daten\src\git
mkdir fo_java
cd fo_java
set SVN_REPO_FO_JAVA=(as in wiki)
// set SVN_REPO_FO_TEST=(as in wiki)
// git svn init --username=tksnp --prefix=origin/ -t tags -b branches -T ao -T trunk -T sparse %SVN_REPO_FO_JAVA%
// git svn init --username=tksnp --prefix=origin/ --tags=/ao --branches=/sparse --trunk=/trunk %SVN_REPO_FO_JAVA%
// git svn init --username=tksnp --prefix=origin/ --branches=/branches %SVN_REPO_FO_JAVA%
// git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA%
git svn init --username=tksnp --prefix=origin/ --trunk=/trunk --tags=/tags --branches=/branches --branches=/ao %SVN_REPO_FO_TEST%

Fetching in steps (until the next author not in the author file is encountered)

First fetch

//git svn fetch --username=tksnp -A.git/authors -r29714:HEAD
//git svn fetch --username=tksnp -A../authors -r731:HEAD
git svn fetch --username=tksnp -A../authors

Subsequent fetches

git svn fetch --username=tksnp -A../authors >> ../fo_test_fetch.txt


### svn config for fo_test

Versuch:

git svn init --username=tksnp --prefix=origin/ --ignore-paths="^(?:AFO|static_files)" %SVN_REPO_FO_TEST% fo_test

corresponding line in .git/config:
    [svn-remote "svn"]
    	ignore-paths = ^(?:AFO|static_files) 

change these to .git/config:

[svn-remote "svn"]
	...
	fetch = trunk:refs/remotes/origin/trunk
	fetch = ao:refs/remotes/origin/ao
	branches = branches/{EmacsNsk,AtmaTester}/*:refs/remotes/origin/branches/*
	tags = tags/*:refs/remotes/origin/tags/*

git svn fetch --username=tksnp -A../authors >> ../fo_test_fetch.txt

takes about 45 minutes for 733 revisions

### svn config for fo_java

two repos: ao and trunk

#### fo_java_trunk

git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA% fo_java_trunk

[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
	include-paths = /cdfa.(?:business|test|utils)/
	fetch = trunk:refs/remotes/origin/trunk

cd fo_java_trunk

git svn fetch --username=tksnp -A../authors >> ../fo_java_fetch.txt 2>&1

(ca 2000-3000 revisions/h)


#### fo_java_ao

git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA% fo_java_ao

[svn-remote "svn"]
	ignore-paths = /(?:valuemaster|legacy)/
	fetch = ao:refs/remotes/origin/ao

git svn fetch --username=tksnp -A../authors >> ../fo_ao_fetch.txt 2>&1


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
