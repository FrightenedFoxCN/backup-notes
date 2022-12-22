# Pro Git book

## Concepts

- Version Control Systems (VCS)

  - local VCS
  - Centralized VCS (CVCS)
  - Distributed VCS (DVCS)

- Snapshots vs. Differences (Git as a stream of snapshots) - Git Branching

- Localized operations

- Integrity - impossible to change the contents of any file or directory without Git knowing about it (SHA-1 hash)

- Generally only adds data

- **Three main states of files**

  - **Modified**: Changed yet not commited

  - **Staged**: Marked to go into the next commit snapshot

  - **Commited**: Safely stored

    <img src="https://git-scm.com/book/en/v2/images/areas.png" style="width:400px;" />

- Basic Git workflow

  1. Modify files in working tree
  2. Selectively state the changes to be part of the next commit, while adding them to staging area
  3. Do a commit

## Basic Configs

- Installation: https://git-scm.com/download/win

- `.gitconfig` in `$HOME` directory or `[path]/etc/gitconfig` as relative to MSys2

- View all the settings with `git config --list --show-origin`

- Set username and email address

  ````powershell
  git config --global user.name "Name"
  git config --global user.email "Address@xxx.com"
  ````

  `--global` option can be override for specific projects with the command without the option in the project

- Set editor

  ```powershell
  git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
  ```

  On a Windows system, if you want to use a different text editor, you must specify the full path to its executable file

- Set default branch name

  ```powershell
  git config --global init.defaultBranch main
  ```

- Check settings

  ```powershell
  git config --list
  ```

  Keys may be seen more than once when different files are read. The last value will be used

  To check specific key, use `git config user.name`

- Getting help

  ```
  git help <verb>
  git <verb> --help
  git <verb> -h
  ```

  The third line is more concise compared with the two above

## Basic Operations

- Getting a repository

  - Take a local directory and turn it into one

    - Use `git init` to create a new subdirectory named `.git` as a skeleton
    - Use `git add <filename>` to specify the files to chect (See below)
    - Use `git commit` to commit (See below)

  - Clone an existing repository

    ```powershell
    git clone https://github.com/libgit2/libgit2 mylibgit
    ```

    The destination name is optional and the default is set to the original one

    `git://` or `user@server:path/to/repo.git` with SSH is also accessible

- Recording changes to the repository

  <img src="https://git-scm.com/book/en/v2/images/lifecycle.png" style="width:400px;" />

  Above shown the lifecycle of the files. Below are commands to help manage it

  - Check the status with `git status`

    - If the files are unmodified, the message will be as follows:

      ````
      On branch master
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working tree clean
      ````

    - If an untracked file (`README` in this case) is in the directory, you'll see:

      ```
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Untracked files:
        (use "git add <file>..." to include in what will be committed)
      
          README
      
      nothing added to commit but untracked files present (use "git add" to track)
      ```

    - If the file is tracked (Staged) but not yet committed, the following message show up:

      ```
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
      
          new file:   README
      ```

    - For not staged file, it shows:

      ```
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)
      
          modified:   CONTRIBUTING.md
      ```

    - When a file is being editted, it will be listed as both staged and unstaged

    - To show a short status, use `git status --short` or `git status -s`, whereas `??` means untracked, `A` means newly added, `<SPACE>M` means modified yet not staged, `M<SPACE>` means modified and staged and `MM` means modified, staged and modified again, i. e. both staged and unstaged

  - Track new files

    ```powershell
    git add <FILENAME>
    ```

  - Ignore files: Create a file named `.gitignore`

    ````
    #files ending in .o or .a
    *.[oa]
    #files ended with a tilde
    *~
    ````

    Rules for `.gitignore` are:

    - Blank lines or lines starting with `#` are ignored

    - Standard glob patterns work, and will be applied recursively
    - Start patterns with a forward slash (`/`) to avoid recursivity
    - End patterns with a forward slash (`/`) to specify a directory
    - Negate a pattern by starting it with an exclamation point (`!`)

  - View staged and unstaged changes

    - `git diff` to show what have been changed but not yet staged
    - `git diff --staged` to show staged changes (also `git diff --cached`)
    
  - Commit changes
  
    ```powershell
    git commit
    ```
  
    To add an commit message inline, use `-m` flag
  
    To automatically stage every track file, add the `-a` option
  
  - Remove files
    
    ```powershell
    git rm <FILENAME>
    ```
    
    If you simply remove the file from your working directory, it is merely unstaged, while `git rm` stages the file's removal
    
    use `--cached` option to keep the file in working tree but remove it from staging area
    
  - Move files
  
    File movement is not explicitly tracked by git, though it can figure out the reneme. `git mv <FORM> <TO>` is equivalent to
  
    ```powershell
    mv <FROM> <TO>
    git rm <FROM>
    git add <TO>
    ```
  
- Viewing the Commit History

  ```
  git log
  ```

  By default, the command lists the commits made in that repository in reverse chronological order with each commit's SHA-1 checksum , the author's name and email, the date written and the commit message. Below list some common options

  - `-p` or `--patch`, showing the difference introduced in each commit

  - `-<NUM>`, limiting the number of log entries displayed

  - `--stat`, showing some abbreviated stats for each commit

  - `--pretty`, changing the log output to formats other than the default, `oneline`, `short`, `full`, and `fuller` are possible option values and can be understood literally. `format` is to specify the format explicitly, e. g.

    ```
    git log --pretty=format:"%h - %an, %ar : %s"
    ca82a6d - Scott Chacon, 6 years ago : Change version number
    085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
    a11bef0 - Scott Chacon, 6 years ago : Initial commit
    ```

    Specifier's are defined as follows:

    | Specifier | Description of Output                           |
    | :-------- | :---------------------------------------------- |
    | `%H`      | Commit hash                                     |
    | `%h`      | Abbreviated commit hash                         |
    | `%T`      | Tree hash                                       |
    | `%t`      | Abbreviated tree hash                           |
    | `%P`      | Parent hashes                                   |
    | `%p`      | Abbreviated parent hashes                       |
    | `%an`     | Author name                                     |
    | `%ae`     | Author email                                    |
    | `%ad`     | Author date (format respects the --date=option) |
    | `%ar`     | Author date, relative                           |
    | `%cn`     | Committer name                                  |
    | `%ce`     | Committer email                                 |
    | `%cd`     | Committer date                                  |
    | `%cr`     | Committer date, relative                        |
    | `%s`      | Subject                                         |

  - `--graph` is used with `format` and `oneline`, as shown the branch and merge history with a little ASCII graph

  - `--abbrev-commit`, showing only the first fiew characters of the SHA-1

  - `--name-only`, showing the list of files modified after the commit information

  - `--name-status`, showing the list of files affected with added/modified/deleted information as well

  - `--oneline`, equal to `--pretty=oneline --abbrev-commit`

  - `--short stat`, showing only the changed/insertions/deletions line from the --stat command

  - `--since`, `--until`, `--after` and `--before` as time-limiting options

  - `--author`, filtering on a specific author

  - `--grep`, search for keywords in the commit messages

  - `committer`, filtering on a specific commiter

  - `-S`, filtering those adding or removing code matching the string

  - `--no-merges`, preventing the display of merge commits
  
- Undoing Things

  ```powershell
  git commit --amend
  ```

  Take your staging area and uses it for the commit, with the previous commit undone
  
  ````powershell
  git reset HEAD <FILE>
  ````
  
  Unstage a staged file
  
  ````powershell
  git checkout -- <FILE>
  ````
  
  Discard the changes you've made
  
  ````powershell
  git restore --staged <FILE>
  git restore <FILE>
  ````
  
  `git restore` is introduced after git version 2.23.0. The first line is to unstage a staged file and the second is to discard the changes you've made

- Working at Remotes

  - Show the remotes

    ````powershell
    git remote
    ````

    `-v` option is used to show the URLs

  - Add remote repositories

    ````powershell
    git remote add <SHORTNAME> <URL>
    ````

  - Fetch and pull

    ````powershell
    git fetch <REMOTE>
    get pull <REMOTE>
    ````

    `git fetch` fetches new work that has been pushed to the server since the last fetch. `git pull` automatically fetch and merge the branch into your current branch

  - Push

    ````powershell
    git push <REMOTE> <BRANCH>
    ````

    Only if you are pushing to a server to which you have write access and if nobody has pushed in the meantime, or you'll be rejected

  - Inspect a remote

    ````powershell
    git remote show <REMOTE>
    ````

  - Rename and remove

    ````powershell
    git remote rename <FROM> <TO>
    git remote remove <REMOTE>
    git remote rm <REMOTE>
    ````

    Once you delete the reference to a remote this way, all remote-tracking branches and configuration settings associated with that remote are also deleted

- Tagging

  - List the tags, in alphebatical order

    ```powershell
    git tag
    ```

    If you're supplying a wildcard pattern to match tag names, the use of `-l` or `--list` is mandatory

  - Create tags

    - Annotated Tags

      ```powershell
      git tag -a <TAG> -m <MESSAGE>
      ```

      Annotated tags are stored as full objects in the Git database. They’re checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG)

      Use `git show <TAG>` to show all information

    - Lightweight Tags

      ```powershell
      git tag <TAG>
      ```

  - Tag later

    ```powershell
    git tag -a <TAG> <PART_OF_CHECKSUM>
    ```

  - Share tags

    ```powershell
    git push <REMOTE> <TAG>
    ```

    If you want to push up a lot of tags, use the `--tags` option:

    ```powershell
    git push <REMOTE> --tags
    ```

  - Delete tags

    ```powershell
    git tag -d <TAG>
    ```

    This does not remove the tag from remote servers. If you want to do so, use the following commands:

    ```powershell
    git push <REMOTE> :refs/tags/<TAG>
    git push <REMOTE> --delete <TAG>
    ```

  - Check out tags

    ```powershell
    git checkout <TAG>
    ```

    With this command you are in "detached HEAD" state. if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash. To make changes, create a branch with option `-b`:

    ```powershell
    git checkout -b <BRANCH> <TAG>
    ```
  
- Aliases
  
  ````powershell
  git config --global alias.<ABBR> <FULL>
  ````
  
  Use `''` for the `<FULL>` if spaces are in between.

## Branching