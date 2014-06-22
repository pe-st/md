git notes
=========

## information commands

- git config -l
- git status
- git remote [-v]

- git log
  git log --pretty=format:"%h %s" --graph
  git log --pretty=format:"%h %an: %s" --all
- git diff HEAD

  The HEAD is a pointer that holds your position within all your different commits.
  By default HEAD points to your most recent commit, so it can be used as a quick
  way to reference that commit without having to look up the SHA.

- git branch


## repositories

- new repo: `git init`
- initial download repo: `git clone <URL>`
- get, don't merge: `git fetch`
- get and merge: `git pull` or `git pull origin master`
- upload: `git push` or `git push -u origin master`
  The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do


## files

- 'stage' a file for commit: `git add <file>`
- unstage a file: `git reset <file>`
- revert a file to the state of the last commit: `git checkout -- <file>`
  (`--` to protect from changing to a branch called `<file>`)
- remove a file from the repo (a branch): `git rm <file>`


## branches

- create a new branch: `git branch <branchname>`
- switch to a branch: `git checkout <branchname>`
- merge a branch into the current branch: `git merge <branchname>`
- delete a branch: `git branch -d <branchname>`
  (if there are unmerged changes: `git branch --force -d <branchname>`)



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
// git svn init --username=tksnp --prefix=origin/ -t tags -b branches -T ao -T trunk -T sparse %SVN_REPO_FO_JAVA%
// git svn init --username=tksnp --prefix=origin/ --tags=/ao --branches=/sparse --trunk=/trunk %SVN_REPO_FO_JAVA%
// git svn init --username=tksnp --prefix=origin/ --branches=/branches %SVN_REPO_FO_JAVA%
git svn init --username=tksnp --prefix=origin/ %SVN_REPO_FO_JAVA%

Fetching in steps (until the next author not in the author file is encountered)

First fetch

git svn fetch --username=tksnp -A.git/authors -r29714:HEAD

Subsequent fetches

git svn fetch --username=tksnp -A.git/authors
