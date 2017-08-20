[TOC]

# Git Command

## Git Basics - Getting a Git Repository
### init



### clone
- `git clone ssh://git@hostname:port/.../xxx.git` - clone the repo from a server whose port is not 22
**example**: 
`git clone ssh://git@10.137.20.113:2222/root/test.git`

## Git Basics - Viewing the Commit History
###log 

**_Table_** Common options to `git log`
**Option**	| **Description**
:----- | ---
`-p              `| Show the patch introduced with  each commit.
`--stat          `| Show statistics for filesmodified   in each commit.
`--shortstat     `| Display only the  changed/insertions/deletions line from the --stat  command.
`--name-only     `| Show the list of files modified  after the commit information.
`--name-status   `| Show the list of files affected  with added/modified/deleted information as well.
`--abbrev-commit `| how only the first fewcharacters   of the SHA-1 checksum instead of all 40.
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
  
  >$ git log --pretty=format:"%h - %an, %ar : %s"
ca82a6d - Scott Chacon, 6 years ago : changed the version number
085bb3b - Scott Chacon, 6 years ago : removed unnecessary test

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
  >  $ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" 
    --before="2008-11-01" --no-merges -- t/
    5610e3b - Fix testcase failure when extended attributes are in use
    acd3b9e - Enhance hold_lock_file_for_{update,append}() API
    f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
    d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
    51a94af - Fix "checkout --track -b newbranch" on detached HEAD
    b0ad11e - pull: allow "git pull origin \$something:\$current_branch" into an unborn branch


## Git Basics - Undoing Things

