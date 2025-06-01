## introduction to git

version control is a system that records changes to a file(s) over time so that you can recall specific versions later.
These versions are recorded in a repository

### types of VS systems:
1. _local VCS:_ all code/changes are tracked in locally in the developers computer
2. _centralised VSC:_ devs connect to a centralised serveR and can collaborate from there
3. _distributed VSC:_ each dev has a local version of the repo. each dev can then interact with the repote repo in various ways

a repo is a directory/folder where the project files are stored. It can either be local or remote

### centralised vs distributed
in centralised VSC commits and updates are done directly to the remote repo

in distributed VSC updates and commits are first done in the local repo before pushing them to the remote repo


### what is git?

Git is a distributed version control tool that allows  each developer in a teach to 
1. sync code from remote repositories
2. create their own local repositories
3. make changes to local repositories
4. interact with corresponding remote repos
5. allow for parallel development with the **branch, merge and rebase** commands

changes made in the remote repo is made instantly available to other devs connected to the repo 

### how does git work?
there are three different local areas within git:
1. working copy/directory
2. staging area
3. local repository

when a file is changed in any way, those changes reside in the working copy

when changes are ready to be commited, they are moved from the working copy to the staging area (temp storage within git)

all commited changes are stored in the local repo

the local repo can be synced with a remote repo

actions git uses with the remote repo include fetch, merge clone push, fetch

### workflow
1. **git add** moves changes from the working directory to the staging area. This staging area is an intermediate/temporary location

2. **git commit** moces changes from the staging area to the local repo

3. **git push** moves the changes from the local repo to the remote repo

4. **git pull** gets the latest version from the remote repo to the local repo

5. **git merge** incorporates changes from the remote repo into the local repo

git setup commands include:

**git init:** used to initialize a local repo

**git clone:** used to create a copy of remote repo in the local machine

**git fork:** create a copy of remote repo in your github account


git sync commands include:

**git origin:** used to connect a remote repo to the local repo with the full command `git remote add origin remote_link`

to rename a remote repo, you can use `git remote rename current_name new_repo_name` e.g. `git remote rename origin cyclops`

to remove a remote repo use `git remote remove repo_name` or `git remote rm repo_name`

to delete a branch in the remote repo, use `git push origin --delete branch_name`

to delete the corresponding branch in the local repo, use `git branch -d branch_name`



to check if the local repo has been linked to a remote repo, we use `git remote -v`, the v flag meaning _verbose mode_

**git pull:** used to copy all files from the _master_ branch of remote repo to local repo with the full command `git pull origin master`

**git push:** used to copy local changes to the remote repo with the command `git push origin master`. ie git push RemoteRepoBranchName LocalRepoBrancHName

when not using vs code, use these steps:
- git init
- git config --global user.name "myname"
- git config --global user.email "email@email.com"


**git status** allows you to see what the local repository looks like

_untracked_ file(s) means that git doesn't know about said files. It means that the file is in the working directory

after doing git commit -m "my message", an output is generated which consists of a branch name, commit id, commit message and the changes made 

`git log` shows you a list of all commits in the current branch

`git log --oneline branch_name` shows a shorted version of the commit list on the given branch

each entry has a number of things
1. a hash id
2. the author associated with the commit
3. the exact time.
4. the commit message

to get greater info about a given commit, use `git show commid_id`

use `git ls-files` to see which files are being tracked in the local repo

## Parallel development

### branching

Git does not create a copy of existing files for a new branch. It points to the snapshot of che changes you have made in the system

development is not usually done on the master/main branch. One codes on separate branches and later merges to the main branch

when one creates a new branch, the new branch will have a copy of all the commit ids present in the source branch

`git branch` lists out all the branches available inside **local repo**. The currently active branch is highlighted with an asterix (*)

`git branch -a` list all the branches, **local and remote** 

`git status` also shows which the currently connected branch is

`git branch branch_name` creates a new branch from the current branch

`git checkout branch_name` is for switching to the mentioned branch

`git log brach_name` lists out all the commits in the mentioned branch

`git rev-list branch_name` shows the number of commits in a given branch

`git push --set-upstream origin branch_name` is used to create a branch name of the given alias in the remote repo if said remote branch doesnt exist


## merging

to copy changes from a branch to the main branch you do the following:

1. go to the branch you want changes to e.g main
2. run `git merge branch_name` to merge changes from the given branch name to the currently connected branch

## rebasing
 redo this section later


## bonus commands

`git archive branch_name --format=zip -o ./archive_name.zip` is used to archive create a zip of the given name from the given branch


`git stash` saves uncommited changes into a temporary location

`git config pull.rebase false`:

**Behavior:**

1. Uses a merge strategy (default in Git).

2. When you run git pull, it performs a git fetch followed by a git merge.

3. Creates a merge commit if the local and remote branches have diverged.

**When to use:**

1. When you want to preserve the entire history, including explicit merge commits.

2. Good for collaborative workflows where tracking merge points is useful (e.g., long-lived feature branches).

`git config pull.rebase true`:

**Behavior:**

1. Uses a rebase strategy.

2. When you run git pull, it performs a git fetch followed by a git rebase.

3. Rewrites local commits on top of the remote branch, avoiding merge commits.

**When to use:**

1. When you want a linear commit history (no merge commits).

2. Preferred for small, frequent updates (e.g., solo work or short-lived branches).

3. Warning: Rebasing rewrites history—avoid if others are working on the same branch.

`git config pull.ff only`:

**Behavior:**

1. Uses a fast-forward-only strategy.

2. When you run git pull, it only updates if the local branch can be fast-forwarded (no diverged commits).

3. Fails if the remote has new commits that require a merge or rebase.

**When to use:**

1. When you want to strictly avoid merges or rebases.

2. Enforces a clean, linear history (e.g., in CI/CD pipelines or maintainer workflows).

3. Requires manual intervention if branches diverge (git merge or git rebase must be done explicitly).


### pull requests
notifies developers about changes you have pushed to a branch in a repo

when a pull request is open, you can aknowlege and review the changes and merge changes to the main branch

Here is the process of creating a pull request on an open source github repo

1. fork the repo
2. clone the repo locally with `git clone https://github.com/your-username/repo.git`
3. add the oiginal repo as upstream with `git remote add upstream https://github.com/original-owner/repo.git`
4. create a new branch in the newly created local repo with `git checkout -b your-feature-branch`
5. make your changes, stage and commit as one usually does
6. before pushing to remote branch, sync with the upstream to avoid conflicts with 
    - `git fetch upstream`
    - `git rebase upstream/main` Or merge: `git merge upstream/main`
7. push to your fork with `git push origin your-feature-branch`
8. open a pull request on the remote fork
9. After entering information, click **create pull request**
10. If approved, the maintainer will merge your PR
11. After the merge, sync your local repo with
    - git checkout main
    - git pull upstream main
    - git push origin main  # Update your fork

### Example Workflow Summary
- git clone https://github.com/your-username/repo.git
- cd repo
- git remote add upstream https://github.com/original-owner/repo.git
- git checkout -b fix-typo
- **Make changes**
- git add .
- git commit -m "Fix typo in documentation"
- git fetch upstream
- git rebase upstream/main
- git push origin fix-typo
- **Then create PR via GitHub UI**


## comparing repos
use the diff command to compare repos using the command `git diff main origin/main`

It can aldo be used to compare branches e.g. `git diff branch_1 branch_2`

It can aldo be used to compare commits e.g. `git diff commit_id_1 commit_id_2`


## fork

this is used to copy anothe repo to your github account

To sync changes made in original repo to your fork, configure a remote that points to upstream repo (the original repo)

use these steps:

use `git remote -v` to list currently configured remote repos

specify a new remote upstream repo that allows syncing the fork with the original repo using `git remote add upstream repo_url`

github workflow

