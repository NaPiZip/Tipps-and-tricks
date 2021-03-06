<img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP.ezVfzOR8He-NjWrfEdl3QQHaHa%26pid%3D15.1&f=1" alt="GitHub logo" height="42px" width="42px" align="left"><br>

# GitHub Notes
<div>
    <a href="https://github.com/NaPiZip/Tipps-and-tricks">
        <img src="https://img.shields.io/badge/Document%20Version-0.0.1-green.svg"/>
    </a>
    <a href="https://www.microsoft.com">
        <img src="https://img.shields.io/badge/Windows%2010%20x64-10.0.17134%20Build%2017134-blue.svg"/>
    </a>
    <a href="https://github.com/">
        <img src="https://img.shields.io/badge/Git%20Version-2.17.1-blue.svg"/>
    </a>
</div>

## How to create and push to a "local" remote repository
This section describes how to set up a "local" remote repository and how to push changes to it. This is helpful if you don't want to push changes to a server, you can create a "local" remote repository on a USB stick or a NAS. This gives you the possibility to back up files within your network.

1. Navigate to the directory where you want to create the "local" remote repository.
```
$ cd remote_repository/
```
2. Initialize a bare git repository.
```
$ git init --bare
Initialized empty Git repository in /e/demo/remote_repository/
```
3. Navigate to the location of the local repository.
```
$ cd local_repository_1/
```
4. Initialize a empty git repository.
```
$ git init
Initialized empty Git repository in /e/demo/local_repository_1/.git/
```
5. Add the remote origin to reference the "local" remote repository.
```
$ git remote add origin ../remote_repository/
```
6. Query the tracked remote repositories in order to verify the success of the previous step.
```
$ git remote -v
origin  ../remote_repository/ (fetch)
origin  ../remote_repository/ (push)
```
7. Create branch of desire.
```
git checkout -b feature1
```
8. Add files to the local repository and commit the changes.
```
$ echo "Text" > example_file.txt
$ git add example_file.txt
$ git commit -m "Created example_file with Text as content."
[feature1 (root-commit) d694ee6] Created example_file with Text as content.
 1 file changed, 1 insertion(+)
 create mode 100644 example_file.txt
```
9. Push changes to user defined branch e.g. `feature1`.
```
$ git push --set-upstream origin feature1
Counting objects: 3, done.
Writing objects: 100% (3/3), 247 bytes | 247.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ../remote_repository/
 * [new branch]      feature1 -> feature1
Branch 'feature1' set up to track remote branch 'feature1' from 'origin'.
```

## How to synchronize with an existing "local" remote repository
The following section describes how to sync with a existing "local" remote repository. This is useful if you want to for example push changes form mutliple locations on your computer or network. In order to refer to how to set it up, see the section above.

1. Navigate to the location for your new local repository.
```
$ cd local_repository_2
```
2. Initialize a empty git repository.
```
$ git init
Initialized empty Git repository in /e/demo/local_repository_2/.git/
```
3. Add the remote origin to reference the "local" remote repository.
```
$ git remote add origin ../remote_repository/
```
4. Query the tracked remote repositories in order to verify the success of the previous step.
```
$ git remote -v
origin  ../remote_repository/ (fetch)
origin  ../remote_repository/ (push)
```
5. Update the local branches.
```
$ git remote update
Fetching origin
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From ../remote_repository
 * [new branch]      feature1   -> origin/feature1
```
6. Checkout the "local" remote branch of desire e.g. `feature1`.
```
$ git checkout feature1
Branch 'feature1' set up to track remote branch 'feature1' from 'origin'.
Switched to a new branch 'feature1
$ cat example_file.txt
Text
```

## How to checkout multiple branches
This section demonstrates how to checkout multiple branches using the `git worktree` feature.

1. Identify the relevant branches.
```
$ git branch -v
feature1 d694ee6 Created example_file with Text as content.
master   fe3906d Created hello_file with Hello as content.
```
2. Use `git worktree` to checkout a additional branch.
```
$ git worktree add ../feature1_branch feature1
Preparing ../feature1_branch (identifier feature1_branch)
HEAD is now at d694ee6 Created example_file with Text as content.
```
3. Verify the result.
```
$ git worktree list
/e/demo/local_repository_2  fe3906d [master]
/e/demo/feature1_branch     d694ee6 [feature1]
```
4. Navigate to desire branch location, add, commit and push changes as desired.

## How to change .sh files to be executable
The following section describes how change the permission settings of a file in order to be a runnable bash script by default.

1. Make sure that the file you want to change contains a shebang, `example.sh`:
```
#!/bin/bash
...
```
2. Type the following command:
```
$ git update-index --chmod=+x example.sh
```
3. Commit the changes as usual.


## Contributing
To get started with contributing to my GitHub repository, please contact me [Slack](https://join.slack.com/t/napi-friends/shared_invite/enQtNDg3OTg5NDc1NzUxLWU1MWNhNmY3ZTVmY2FkMDM1ODg1MWNlMDIyYTk1OTg4OThhYzgyNDc3ZmE5NzM1ZTM2ZDQwZGI0ZjU2M2JlNDU).
