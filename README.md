# Git and GitHub course notes

### How Git Works

Git controls all modificantions in the files of the repository, creating a history of changes that the files has passed by over the time.

Git has 3 basic stages:
  1. Working tree
    Here are the files you are editing and modifying at te moment.
  2. Stage
    Here are the files you finish modifying and are ready to be commited
  3. HEAD
    Here is the files you already commited.

Git workflow to consolidate your changes to HEAD, is:
  1. finish your changes and save the file.
  2. add the file(s) to stage area (git add)
  3. commit these changes (git commit)

You can literally see how git works using https://git-school.github.io/visualizing-git/.
## Branches

Git allows you to create branches to split the work you've to do. Usualy the main branch, that will contains all the consolidated changes is MASTER.
When you create a branch, git will create another line, as the follow exemple:
```
master
(HEAD)
   |──── branch01
             |──── branch01.1
   |──── branch02
```
In this case, the changes you do on the other branches (branch01 and branch01.1), will not be in master and vice versa.
See the commands to work with branches on line 99.

It is very important to slpit the development in branches. This way what a Developer01 is working on (on branch feature01) does not affect the changes
Developer02 is doing on branch feature02. Both branches are isolated and the changes will not overwrite it selves.

When the feature developed on feature01 is done, you join it on branch master using the command git merge.

 - **HEAD**: the HEAD shows where your repository is. It will be always the last commit you did.
### Conventions

- Commit
  - The commit should contains a small bunch of changes or a feature (or a significant part of it). So if you have big changes to make, split it in smalls changes
  - **Avoid commits with too much changes.** Split the changes into small changes when it is possible.
  - The commit message should be a short, but clear, message that shows what changes that commit contains.
  - When to commit your code?
    That depends on how each team works, but in general, we should follow some tips:
    - Commit your code when a bug is fixed. If it is a big fix, try to split it into small pack of changes to commit inparts (changes in one file, for exemple)
    - Commit it when you add a small new feature, or when a small part of a big new feture is done.
    - When our code is in a state that you would like to remember.
    - **You should not commit code that doesn't work**. Altought is not recommended to olnly commit in the endo of a feature/bug fix.

### General Commands

- git init
This command initialize the current folder as a git repository to git start tracking it.

- git init --bare
This command do the same as git init but it creates a repository that will cointaisn only the changes of the files and not a copy of the files it self.
It means that we won't use it to access and change files. It is just to store the changes. It's used to create remte repositories.

- git remote
It lists all the remote repositories of the repo you're in. Will show blank if there is none.

- git add
This command add the files to the stage area. This area holds the files selected to be commited
E.g.:
  - git add <file-name>
    > add an specific file. You can put more files
  - git add .
    > add all files in the current directory

- git commit
his command consolidate your changes in a "package" and we used to put some short message.
E.g.:
  - git commit -m 'Your message here'

- git status
Show the status of the branch you are in.

- git log
Shows you all the history that already occured in your repository. See http://devhints.io/git-log to have some tips and how to use it.
  - git log --oneline
    >Shows you a simplified log with short has and message of the commit.
  - git log -n X
    >Shows you the last X commits

- .gitignore (file)
You can make Git to ignore some file or folders. You just need to add a special file named .gitignore to your project.
In these, file you just add the the files and folder (using / at the end) that you don't want git tracks.
So now, if you type git status, git won't show you to commit the files or folders you setto ignore.
Altough git won't track these files, it will show you to commit the .gitignore file.

- git remote add
This command adds a remote repository to your local repository
  - the command should have a name and the address of the remote repository (URL, lan address, local).
  E.g.: git remote add name_remote https://remote_repo.com.br/address.

- git push
This command pushes your changes to the remote server you configure as remote
E.g.: git push remote_name_you_gave_when_add_remote branch_you_want_to_push

- git pull
This command gets the data of the remote repositori and brings to your local branches
**By default, when you clone a remote repository, git name it remote as ORIGIN.** To change it use git remote rename old_name new_name
E.g.: git pull remote_repository_name branch_name (optional)

- git clone
Used to make a copy of the remote repository you want
E.g.:
  - git clone https://remote_repo.com.br/address folder_name_you_want_create (optional)

- git branch commands
  - git branch
    >List all the branches you have on your repository.
  - git branch branch_name
    >Create a new branch with the name you gave it on branch_name
  - git switch branch_name or git checkout branch_name
    >Change the repository you're working on to the branch_name repository
  - git checkout <u>**-b**</u> branch_name
    >Creates a new branch and change to the new branch.

- git merge
This command take one branch and put it inside another.
E.g.: git branch01 branch02
>For exemple: you finished a feature on branch new_module and need to put these changes on branch master.
>So you checkout to the branch you want merge new_module into (master) and there you execute the following command:
  - git merge master new_module


- git rebase
This command takes the commits of the branch origin and put behind on the branch you you're rebasing.
**BE CAREFUL**: could make you lose the work.
  - git rebase branch_name
  >it will bring branch_name commits to be the base of the branch you're in.

- undoing changes (ctrl + Z)
  - **git checkout -- file_name**
  >reverting what is in the working tree (not staged or commited):
  - **git reset HEAD** You can use an specific commit instead of HEAD
  >reverting what you've already add to stage:
  - **git revert commit_hash**
  >reverting whatyou already have commited:

- git stash
Git Stash will "save" your changes in a temporary stack (aside the main stack of your project) and won't show it in your git log.
  - **git stash**
    >This command will "commit" your changes to the stash area. You can set a message to this stasj. Just type it after the word stash
  - **git stash list**
    >This command will list all you have on stash area by a number into {}
  - **git stash apply**
    >This command will restore the last thing you stashed. You can apply a specific stash by informing the stash number (see git statsh list).
  - **git stash drop**
    >This command will discard the last thing you stashed. You can drop a specific stash by informing the stash number (see git statsh list).
  - **git pop**
    >This command will execute a stash apply followed by a stash drop. You can use it to restore a specific stash by informing the stash number (see git statsh list).

- Navigate through commits
Using Git, you can navigate through commits an restore you project to an specific commit.
  - **git checkout commit_hash**
    >By using this command you set HEAD of your project to the commit you want.
    >**OBS:** when use git checkout commit_hash, you are **deatached** of the main source control. That is, you're not in any branch.
    >So, if you make a commit here and change to MASTER, these commits will be lost and you couldn't retrive in in the future.
    >If you want to make these commit achieveble, you have to **create a new branch** after moving ead to the commit you want.
  - **git checkout -b new_branch**
    >This way, this new_branch is based on the commit you've checkout out before.

- git diff
This command is used to see the changes between 2 commits or a commit and working tree
  - **git diff**
    >This command will show the differences between the last commit and your unstaged changes. If you stage it, it won't show anything.
  - **git diff old_hash_commit..new_hash_commit**
    >Here we can see the differences between 2 commits. The .. can be translate as until. So, by using this command, you're able to see all the changes occured bewteen these commits. You can also use only **git diff old_hash_commit** to compare with HEAD.

- git tag
You can create a tag, a mark on the history of your project for a version release for exemple
  - **git tag -a tag_name**
    >This command will create a tag in HEAD. You can also set a message to this tag using -m 'message'.
    >You can create a tag on a specific commit to.
    >When you use github, these tag will apperar in RELEASE and can be downloaded.
  - **git push origin tag_name**
    >This command will push your tags to the remote server.
  - **git tag**
    >This commnand lists all the tags you have.
  - **git checkout tag_name**
    >You can also checkout your project to a specific tag. Use this command to do it.