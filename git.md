git notes
=========

## information commands

- `git config -l` (all entries) or `git config --global -l` (only entries from global config)
- `git status`
- `git remote [-v]`

- `git log`
  Uses the default log format (see format.pretty)
  `git log --all`
  `git log --pretty=format:"%h %s" --graph`
  With author date and name
  `git log --pretty=format:"%h %ai %an: %s" --all`
  With author date and email
  `git log --pretty=format:"%h %ai %ae: %s" --all`
  With complete hash and the internal date format
  `git log --pretty=format:"%H %ad %ai %an: %s" --date=raw --all`

  More examples
  `git log --graph --all --pretty=format:'%C(yellow)%h%C(cyan)%d%Creset %s %C(white)- %an, %ar%Creset'`
  `git log --color --graph --pretty=format:'%C(bold white)%h%Creset -%C(bold green)%d%Creset %s %C(bold green)(%cr)%Creset %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative`
  `git log --color --graph --pretty=format:'%C(bold white)%H %d%Creset%n%s%n%+b%C(bold blue)%an <%ae>%Creset %C(bold green)%cr (%ci)' --abbrev-commit`

- `git branch` or `git branch --all`
- `git remote` or `git remote -v`

- `git show-ref`


## Config

There are four (five) places where Git checks for settings (in order of precedence):

- super      : `%PROGRAMDATA%\Git\config` (machine specific settings on Windows; in modern Windows' this is `%SystemDrive%\ProgramData`, earlier `C:\Users\All Users`)
  (the name 'super' is not official, but used by SmartGit in its logfiles)
- 'system'   : `$(prefix)/etc/gitconfig` (machine specific, on Windows installation specific, e.g. `C:\Daten\P\Git\mingw64\etc\gitconfig`)
- xdg global : `$XDG_CONFIG_HOME/git/config` or `$HOME/.config/git/config` (user global like 'global', but overwritten by 'global')
  (XDG stands for freedesktop.org, formerly X Desktop Group; XDG_CONFIG_HOME: should default to `$HOME/.config`)
- 'global'   : `~/.gitconfig` (user specific)
- 'local'    : `.git/config` in the current repo

Too see all configs including their source (since Git 2.8):
`git config --list --show-origin`

3 of the above places can explicitly specified to the `git config commands` with `--system`, `--global` and `--local`, resp.


See also:

    http://stackoverflow.com/questions/17756753/where-do-the-settings-in-my-git-configuration-come-from/35670933#35670933
    http://stackoverflow.com/questions/34111522/why-git-config-list-total-is-not-the-same-as-system-global-local/34112678


## Diffing

- `git diff` : shows what is not added yet
- `git diff --cached` : shows what would be committed
- `git diff --staged` : synonym to --cached
- `git diff HEAD` : difference of workspace to HEAD (staged and unstaged)

Use `git difftool` instead of `git diff` to use an external diff tool (e.g. Beyond Compare)


## glossar

- The HEAD is a pointer that holds your position within all your different commits.
  By default HEAD points to your most recent commit, so it can be used as a quick
  way to reference that commit without having to look up the SHA.





## repositories

- new repo: `git init`
  (or: `git init --bare reponame.git`)
- initial download repo: `git clone <URL>`
  or `git clone -b <branch> <URL>`
- get, don't merge: `git fetch`
- get and merge: `git pull` or `git pull origin master`
  - without automatic commit: `git pull --rebase`
    (or: `git pull --no-commit` )
  - remember this behaviour: `git config --global branch.autosetuprebase always`
- upload: `git push` or `git push -u origin master`
  The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do
- if the (current) branch isn't tracked (you forgot `-u` when pushing):
  `git branch -u origin/master`
- stop tracking a branch (e.g. branch 'win') and delete the local branch:
  `git config --unset branch.win.remote`
  `git config --unset branch.win.merge`
  `git branch -d win`


### import local repo in GitHub

git clone --bare --no-hardlinks file:///Users/pesche/Documents/dev/git/gugus/emacs.d
cd emacs.d.git
git push --mirror https://github.com/pe-st/dot-e.git

### clone into existing directory

Clone into new directory, mv the .git folder


### remotes

- remotes have a name, default name (when you clone a repo) is `origin`
- multiple remotes are possible, list of remotes:
  `git remote -v` (-v adds the URLs to the output)
- the remotes can also be seen with `git show-ref`

create a new remote for an existing local repo:
- on the remote:
  `git init --bare jboss_standalone.git`
- on the local:
  `git remote add origin file:////DOMAIN/network/path/to/jboss_standalone.git`
  `git push origin master`

add/delete/replace remote

- `git remote add origin <URL>`
- `git remote rm origin`
- `git remote set-url origin <URL>`

#### add second remote repo

- `git remote add upstream https://github.com/docToolchain/docToolchain.git`
- set tracked branch of local master to upstream/master (instead of origin/master)
- pull (from upstream) and then "push to" origin/master from local master


#### git-svn remotes

- don't show up with `git remote`
- can be seen with `git show-ref`
  -> they are just branches



## files

- 'stage' a file for commit: `git add <file>`
- unstage a file: `git reset <file>`
- revert a file to the state of the last commit: `git checkout -- <file>`
  (`--` to protect from changing to a branch called `<file>`)
- remove untracked files: `git clean --dry-run -f` then `git clean -f`
- remove a file from the repo (a branch): `git rm <file>`
- commit what is staged: `git commit -m "comment"`
- update last commit with stage: `git commit --amend`
- revert a file to a historic state: `git checkout <commit>`


### line endings

https://help.github.com/articles/dealing-with-line-endings/

After changing the line endings in `core.autocrlf` or `.gitattributes` repopulate the workspace:

`git rm --cached -r .`
`git reset --hard`

#### line endings for individual files

Define explicit rules in `.gitattributes`, e.g.:

    # Files that Sublime writes as LF even on Windows
    Package[[:space:]]Control.sublime-settings text eol=lf
    Preferences.sublime-settings text eol=lf

Note how you have to escape whitespace inside a file name (!)

Another way to adjust your workspace to a changed `.gitattributes` (see also above, this one is from
https://help.github.com/articles/dealing-with-line-endings/#refreshing-a-repository-after-changing-line-endings):

- backup and remove all 'changed' files in the workspace
- `rm .git/index`
- `git reset`
- restore the files


## branches

- create a new branch: `git branch <branchname>`
  . not from HEAD: `git branch <branchname> <commit>`
- switch to a branch: `git checkout <branchname>`
- local branch from remote branch (tracking branch): `git checkout -b <branchname> origin/<branchname>`
  or `git checkout --track origin/<branchname>`
- combine creation/switch: `git checkout -b <branchname>`
- merge a branch into the current branch: `git merge <branchname>`
- delete a branch: `git branch -d <branchname>`
  (if there are unmerged changes: `git branch --force -d <branchname>`)
- delete a remote branch: `git push origin :<branch>`
- diff two branches: `git diff master..<branchname>`
  or `git diff --name-status master..<branchname>`

### under the hood

Branches are stored in .git/refs

'refs' are References: a file per branch that contains just the SHA value of the last commit

- master is in .git/refs/heads/master (i.e. it's just a local branch called 'master')
- local branches are in .git/refs/heads/<localbranch>
- remote branches are in .git/refs/remotes, e.g. .git/refs/remotes/origin/trunk


### merge

- fast forward: current branch had no modifications after the branching point
- `git merge oss` merges the branch `oss` into the current branch and commits (if no conflicts)
- `git merge --no-commit --no-ff oss` merges the branch `oss` into the current branch, but does not commit
- edit conflict with Beyond Compare: `git mergetool`
- `git merge --abort` abort a merge with conflicts
- `git merge --squash master` merges all commits from master into the current branch into one commit

### rebase

- `git rebase oss` 'moves' the commits of branch `oss` onto the current branch



### compare branches

- simple with SourceTree (right-click on a branch, "Diff against current")
- Merge without commit (see above)

### cherry pick

- `git cherry-pick --no-commit f4343dc...` Copy one individual commit from another branch to the current one:

### track/pull all branches

    git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
    git fetch --all
    git pull --all

## tags

Two flavours: annotated and lightweight

    Basically, lightweight tags are just pointers to specific commits. No further information is saved; on the other hand, annotated tags are regular objects, which have an author and a date and can be referred because they have their own SHA key.

    If knowing who tagged what and when is relevant for you, then use annotated tags. If you just want to tag a specific point in your development, no matter who and when did that, then lightweight tags are good enough.

- display tags: `git tags`
- display the tag annotations (if any): `git show <tagname>`
- create an annotated tag: `git tag -a <tagname> -m 'message'`
- create a lightweight tag: `git tag <tagname>`
- push a tag or all tags to the remote repo: `git push origin <tagname>` or `git push origin --tags`
  (for git 1.8.3 and later: `git push --follow-tags` pushes tags and commits simultaneously)
- "check out" a tag (more like creating a branch at a tag): `git checkout -b <branch> <tagname>`

### create a tag for every branch

    git branch | while read remote; do git checkout "$remote"; git tag "$remote"; done


## stash

- store away some patches: `git stash`
- show available stashes: `git stash list`
- show the content of a stash: `git stash show -p`
- apply a stash: `git stash apply`
- apply a stash and drop it: `git stash pop`
- drop a stash: `git stash drop`


## Configuration

- `git config --global --unset format.pretty` Deletes a config (here pretty.format)

### Proxy

- `git config --global http.proxy http://localhost:3128`
- `git config --global https.proxy http://localhost:3128`

### Email

- `git config --global user.name "Peter Steiner"`
- `git config --global user.email unistein+reinette@gmail.com`

### Pretty Format

- `git config --global format.pretty "format:%h %ai %ae: %s"`

### Aliases

- `git config --global alias.l "log --color --pretty=format:'%h %C(green)%ai%Creset %C(yellow)%ae%Creset %s%C(red)%d%Creset'"`
  (on windows `yellow` is more readable than `blue`)

### Follow Renames

- `git config --global log.follow true`


## Git LFS

- Muss separat installiert werden (Mac: brew install git-lfs)
- Benötigt Server-Unterstützung (zB GitHub, GitLab, Bitbucket Cloud, Bitbucket Server)
- `git lfs version`
- `git lfs track`
- `git lfs ls-files`


## Git Dojo

- Git Commandline (Editor-Variable?)
- GitHub zeigen (Vorbereitung: Account anlegen)
- GUI zeigen
- Beyond Compare Integration
- Workflow
- Tutorials: atlassian, git-scm, rogerdudler, gitimmersion

### Aufgaben

- Initiale Config
  - Email-Adresse
  - CNTLM
- Commits auf origin/master und im lokalen Repo
  - was passiert bei pull mit und ohne revert?
- auf origin/master hat jemand Files gelöscht: wie reparieren?
  - git clone
  - git revert
  - git push
  - vgl. http://christoph.ruegg.name/blog/git-howto-revert-a-commit-already-pushed-to-a-remote-reposit.html


## SSH

### SSH with PLink

- set GIT_SSH=C:\Daten\P\putty\PLINK.EXE
- load the private key (.ppk) into pageant
- setup a PuTTY Session and connect once to store the server fingerprint
- git clone ssh://<putty-session-name>/path/to/repo


## Rewriting History

### fix last (non-pushed) commit

- fix the files
- stage the files
- `git commit --amend`

### change the date of the last commit

The author date:
`git commit --amend --date="Thu Aug 13 22:56 2015 +0200"`

Both dates:
`GIT_COMMITTER_DATE="Thu Aug 13 22:56 2015 +0200" git commit --amend --date="Thu Aug 13 22:56 2015 +0200"`

### changing commit date for all commits

```
$ git filter-branch -f --env-filter '
export GIT_COMMITTER_DATE="$GIT_AUTHOR_DATE"' HEAD
```

### changing wrong author info

```
git filter-branch --env-filter '
    if test "$GIT_AUTHOR_EMAIL" = "tksnp@..."
    then
        GIT_AUTHOR_EMAIL=unistein+n32393@gmail.com
        export GIT_AUTHOR_EMAIL
    fi
    if test "$GIT_COMMITTER_EMAIL" = "tksnp@..."
    then
        GIT_COMMITTER_EMAIL=unistein+n32393@gmail.com
        export GIT_COMMITTER_EMAIL
    fi
    if test "$GIT_AUTHOR_NAME" = "unknown"
    then
        export GIT_AUTHOR_NAME="Peter Steiner"
    fi
    if test "$GIT_COMMITTER_NAME" = "unknown"
    then
        export GIT_COMMITTER_NAME="Peter Steiner"
    fi
' -- --all
```

If all went well: remove the backup from filter-branch
- `git update-ref -d refs/original/refs/heads/master`
- `git update-ref -d refs/original/refs/remotes/origin/master`

If you have to push it (be careful here, your coworkers won't like this!)
- `git push --force --dry-run`
- `git push --force`

Your coworkers must pull it with rebasing!
- `git pull --rebase`


## Tools

### msysgit (Git for Windows 1.9.5)

- change home directory from `U:/` to `c:/Daten/P/Git/home/pesche/` :
  - mkdir `home/pesche` inside the Git installation (`c:/Daten/P/Git` for me)
  - edit `c:/Daten/P/Git/etc/profile` : replace `HOME="$(cd "$HOME" ; pwd)"` with `HOME="/home/pesche"`


### SourceTree

- embedded Git location:
  - %USERPROFILE%\AppData\Local\Atlassian\SourceTree\git_local


### SmartGit

- configure .gitconfig location in file %APPDATA%\syntevo\SmartGit\<major-smartgit-version>\smartgit.properties
  (see https://www.syntevo.com/doc/display/SG/System+Properties)

    smartgit.executable.home=c:/Daten/P/SmartGit/home
- Preferences Dialog is in Edit Menu (WTF?)
  - set the path to git.exe

#### Features

- has not only Git FLow, but also Git Flow Light
- Graphical Log allows to show/hide each branch separately


### JetBrains IntelliJ IDEA



### Beyond Compare

- This is for all platforms
  git config --global diff.tool bc3
  git config --global merge.tool bc3
  git config --global difftool.prompt false

- This is for Windows only (Linux / Mac assume /usr/local/bin/bcomp)
  git config --global difftool.bc3.path "c:/Program Files (x86)/Beyond Compare 3/bcomp.exe"
  git config --global mergetool.bc3.path "c:/Program Files (x86)/Beyond Compare 3/bcomp.exe"


#### for TortoiseGit

- Settings/Diff Viewer  : `"C:\Program Files (x86)\Beyond Compare 3\BComp.exe" %base %mine /title1=%bname /title2=%yname /leftreadonly`
- Settings/DV/Merge Tool: `"C:\Program Files (x86)\Beyond Compare 3\BComp.exe" %mine %theirs %base %merged /title1=%yname /title2=%tname /title3=%bname /title4=%mname`

#### for SourceTree (Windows)

Tools / Options / Diff : just select Beyond Compare in the dropdowns for external Diff/Merge


## Forks and Pull Requests

Pull from a fork on GitHub

    git pull https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git BRANCH_NAME

Pull a pull request (with numerical id ID) from GitHub

    git pull https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git pull/ID/head

Note that you better checkout first the commit where the PR should apply...

Sync a fork on GitHub

    git clone https://github.com/YOUR_USERNAME/YOUR_FORK.git
    cd YOUR_FORK
    git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
    git fetch upstream
    git checkout master
    git merge upstream/master
    git push


## SVN

cloning of fo_java since the creation of the ao directory (SVN 29714)

### git svn for a repo where trunk/branches/tags are not at the root

git svn init --trunk=$SVN_PATH/trunk --branches=$SVN_PATH/branches --tags=$SVN_PATH/tags $SVN_URL $GIT_REPO_NAME

is the same as

git svn init -s $SVN_URL/$SVN_PATH $GIT_REPO_NAME


### using the prefix option

--prefix=origin/
... is the default for newer git versions

http://blog.tfnico.com/2013/08/always-use-git-svn-with-prefix.html

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

    [svn-remote "svn"]
        ignore-paths = /(?:valuemaster|legacy)/
    #   fetch = ao:refs/remotes/origin/ao
    # wildcards don't work with fetch
    #   fetch = ao/*/trunk:refs/remotes/origin/ao/trunk/*
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
    #   branches = ao/*/branches:refs/remotes/ao/branches/*
    #   tags = ao/*/tags:refs/remotes/ao/tags/*

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
