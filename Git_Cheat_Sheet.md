# Git
----

[TOC]

# 2. Git Basics

## 2.1 Getting a Git Repository
### init

### clone
- `git clone ssh://git@hostname:port/.../xxx.git` - clone the repo from a server whose port is not 22
**example**: 
`git clone ssh://git@10.137.20.113:2222/root/test.git`

## 2.2 Recording Changes to the Repository


## 2.3 Viewing the Commit History
### log 

**_Table_** Common options to `git log`

**Option**	| **Description**
:----- | ---
`-p              `| Show the patch introduced with  each commit.
`--stat          `| Show statistics for filesmodified   in each commit.
`--shortstat     `| Display only the  changed/insertions/deletions line from the --stat  command.
`--name-only     `| Show the list of files modified  after the commit information.
`--name-status   `| Show the list of files affected  with added/modified/deleted information as well.
`--abbrev-commit `| Show only the first fewcharacters   of the SHA-1 checksum instead of all 40.
`--relative-date `| Display the date in a relative  format (for example, “2 weeks ago”) instead of using  the full date format.
`--graph         `| Display an ASCII graph of the  branch and merge history beside the log output.
`--pretty        `| Show commits in an alternateformat. Options include oneline, short, full, fuller, and format (where you specify your own format).


- `git log -p -2` - list commit logs, `-p` for detailed changes, `-2` for limiting the output to only the last two entries
- `git log --stat` - see some abbreviated stats for each commit
- `git log --pretty=oneline` - pretty print log. 
`oneline`, `short`, `full`, and `fuller`
- `git log --pretty=format`

  **Option** | 	**Description of Output** 
  :---:| ---
  `%H `| Commit hash
  `%h `| Abbreviated commit hash
  `%T `| Tree hash
  `%t `| Abbreviated tree hash
  `%P `| Parent hashes
  `%p `| Abbreviated parent hashes
  `%an`| Author name
  `%ae`| Author email
  `%ad`| Author date (format respects the --date=option)
  `%ar`| Author date, relative
  `%cn`| Committer name
  `%ce`| Committer email
  `%cd`| Committer date
  `%cr`| Committer date, relative
  `%s `| Subject
  
  > ``` git
  > $ git log --pretty=format:"%h - %an, %ar : %s"
  > ca82a6d - Scott Chacon, 6 years ago : changed the version number
  > 085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
  > ```

- `git log --pretty=format:"%h %s" --graph` -adds a nice little ASCII graph showing your branch and merge history


- **_Table_** 3. Options to limit the output of `git log`

  **Option** |	**Description**
  :--- | :---
  `-(n)              `| Show only the last n commits
  `--since, --after  `| Limit the commits to those made after the specified date.
  `--until, --before `| Limit the commits to those made before the specified date.
  `--author          `| Only show commits in which the author entry matches the specified string.
  `--committer       `| Only show commits in which the committer entry matches the specified string.
  `--grep            `| Only show commits with a commit message containing the string
  `-S                `| Only show commits adding or removing code matching the string

  - `git log --since=2.weeks`
  - **example**:
    >  ``` git
    > $ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" --before="2008-11-01" --no-merges -- t/
    > 5610e3b - Fix testcase failure when extended attributes are in use
    > acd3b9e - Enhance hold_lock_file_for_{update,append}() API
    > f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
    > d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
    > 51a94af - Fix "checkout --track -b newbranch" on detached HEAD
    > b0ad11e - pull: allow "git pull origin \$something:\$current_branch" into an unborn branch


## 2.4 Undoing Things

- `git commit --amend` - all you’ll change is your commit message.
- example:
  > ``` git
  > $ git commit -m 'initial commit'
  > $ git add forgotten_file
  > $ git commit --amend
  > ```

  You end up with a single commit – the second commit replaces the results of the first.

- `git reset HEAD <file>...` - unstage a staged file.
- `git checkout -- <file>...` - revert file back to what it looked like when you last committed. **_DANGEROUS!_** Better to use <a name="2.4_git_checkout">[Git Branching<sup>[1]</sup>](#3-git-branching).</a>

## 2.5  Working with Remotes

### remote

- `git remote -v` - shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote
- `git remote add <shortname> <url>` - add a new remote Git repository as a shortname you can reference easily
- example:
  > ```git
  > $ git remote add pb https://github.com/paulboone/ticgit
  > $ git remote -v
  > origin	https://github.com/schacon/ticgit (fetch)
  > origin	https://github.com/schacon/ticgit (push)
  > pb	https://github.com/paulboone/ticgit (fetch)
  > pb	https://github.com/paulboone/ticgit (push)
  > ```

- `git fetch [remote-name]` - only downloads the data to your local repository – it doesn’t automatically merge it with any of your work or modify what you’re currently working on. You have to merge it manually into your work when you’re ready.

- `git push [remote-name] [branch-name]` - If you want to push your master branch to your `origin` server. Usually, 
  > ``` git
  > $ git push origin master
  > ```

- `git remote show [remote-name]` - see more information about a particular remote. Usually, 
  > ``` git
  > $ git remote show origin
  > ```

- `git remote rename` 
  > ``` git
  > $ git remote rename pb paul
  > $ git remote
  > origin
  > paul
  > ```

- `git remote remove` or `git remote rm`:
  > ``` git
  > $ git remote remove paul
  > $ git remote
  > origin
  > ```

## 2.6 Tagging

- `git tag` - list all git tags.
- `git tag -l "v1.8.5*"` - only interest in v1.8.5*

Git uses two main types of tags: **lightweight** and **annotated**.

**Annotated Tags**

- `git tag -a v1.4 -m "my version 1.4"` - The -m specifies a tagging message, which is stored with the tag.
- `git show v1.4` - show the information of v1.4.

**Lightweight Tags**

- `git tag v1.4-lw` - create a lightweiight tag v1.4-lw.

**Tagging Later**

> ``` git
> $ git log --pretty=oneline
> 15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
> a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
> 0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
> 6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
> 0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
> 4682c3261057305bdd616e23b64b0857d832627b added a todo file
> 166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
> 9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
> 964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
> 8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme
> ```

- `git tag -a v1.2 9fceb02` - tag the submitted commit.

**Sharing Tags**

Tags need to be pushed explicitly.

- `git push origin v1.5` - push one tag.
- `git push origin --tags` - push all the tags.

**Checking out Tags**

- `git checkout -b [branchname] [tagname]` - <br> e.g.
  > ``` git
  > $ git checkout -b version2 v2.0.0
  > Switched to a new branch 'version2'
  > ```

## 2.7 Git Aliases

Examples:
> ``` git
> $ git config --global alias.co checkout
> $ git config --global alias.br branch
> $ git config --global alias.ci commit
> $ git config --global alias.st status
> ```

> ``` git
> $ git config --global alias.unstage 'reset HEAD --'

The above makes the following equivalent.

> ``` git
> $ git unstage fileA
> $ git reset HEAD -- fileA
> ```

Show the last.
> ``` git
> $ git config --global alias.last 'log -1 HEAD'
> ```

**Run an external command**

start the command with a ! character.

`git config --global alias.visual '!gitk'`


 


# 3. Git Branching

[Back to 2.4<sup>[1]</sup>](#2.4_git_checkout)

## 3.1/3.2 Basic Branching and Merging

``` git
$ git checkout -b iss53
Switched to a new branch "iss53"
```

This is shorthand for (make a branch and switch to it):

``` git
$ git branch iss53
$ git checkout iss53
```

- `git merge <branch_name>` merge <branch_name > to the current branch.
- `git branch -d <branch_name>` delete the branch <branch_name>

## 3.3 Branch Management

- `git branch` - list all branches.
- `git branch -v` - to see the last commit on each branch.
- `git branch --merged` - To see which branches are already merged into the branch you’re on.
- `git branch --no-merged` - To see all the branches that contain work you haven’t yet merged in.

## 3.4/3.5 Branching Workflows / Remote Branches

- `git fetch origin` - fetches any data from server that you don’t yet have, and updates your local database. 

  ![git fetch][remote-branches-3]

- `git push origin serverfix:awesomebranch` - push your local serverfix branch to the awesomebranch branch on the remote project
- `git checkout -b [branch] [remotename]/[branch]` equals `git checkout --track [remotename]/[branch]` - local brach [branch] will track [remotename]/[branch], just like the local master tracks origin/master when you clone a repo with the default setting.
- `git checkout -b sf origin/serverfix` - set up a local branch with a different name than the remote branch.
- `git branch -u origin/serverfix` - If you already have a local branch and want to set it to a remote branch you just pulled down, or want to change the upstream branch you’re tracking, you can use the -u or --set-upstream-to option to git branch to explicitly set it at any time.
- `git merge @{u}` / `git merge @{upstream}` - equals `git merge origin/master`.
- `git branch -vv` - list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both.
  > ``` git
  > $ git branch -vv
  > iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets
  > master    1ae2a45 [origin/master] deploying index fix
  > * serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
  > testing   5ea463a trying something new
  > ```

- `git fetch --all; git branch -vv` - If you want totally up to date ahead and behind numbers, you’ll need to fetch from all your remotes right before running this.
- 

**Pulling**

> Generally it’s better to simply use the fetch and merge commands explicitly as the magic of git pull can often be confusing.

**Deleting Remote Branches**

`git push origin --delete serverfix` - Basically all this does is remove the pointer from the server. The Git server will generally keep the data there for a while until a garbage collection runs, so if it was accidentally deleted, it’s often easy to recover.

## 3.6 Rebasing

**Basic merge process**:

![Simple divergent history][basic-rebase-1]

![Merging to integrate diverged work history][basic-rebase-2]

**Rebasing**:

> ``` git
> $ git checkout experiment
> $ git rebase master
> First, rewinding head to replay your work on top of it...
> Applying: added staged command
> ```

![Rebasing the change introduced in C4 onto C3][basic-rebase-3]

> ``` git
> $ git checkout master
> $ git merge experiment
> ```

![Fast-forwarding the master branch][basic-rebase-4]








```
fef
f
f
f
f
f
ff
f
ff

f
f

f
f
f
f
f

f

ff

f
fd
fds
f
sdf

fd
fd
fd
f
d
fd
f
```

[remote-branches-3]:  ./pics/Git/remote-branches-3.png
[basic-rebase-1]: ./pics/Git/basic-rebase-1.png
[basic-rebase-2]: ./pics/Git/basic-rebase-2.png
[basic-rebase-3]: ./pics/Git/basic-rebase-3.png
[basic-rebase-4]: ./pics/Git/basic-rebase-4.png

