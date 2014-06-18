git notes
=========

## information commands

- git config -l
- git status
- git remote [-v]



## repositories

- new repo: `git init`
- initial download repo: `git clone URL`
- get, don't merge: `git fetch`
- get and merge: `git pull`
- upload: `git push`


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
