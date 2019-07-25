<img src="https://www.bazel.build/images/bazel-icon.svg" alt="Bazel logo" height="42px" width="42px" align="left"><br>

# Bazel Notes
<div>
    <a href="https://github.com/NaPiZip/Tipps-and-tricks">
        <img src="https://img.shields.io/badge/Document%20Version-0.0.1-brightgreen"/>
    </a>
    <a href="https://www.microsoft.com">
        <img src="https://img.shields.io/badge/Windows%2010%20x64-10.0.17134%20Build%2017134-blue.svg"/>
    </a>
    <a href="https://www.bazel.build">
        <img src="https://img.shields.io/badge/Bazel%20Version-0.0.28-blue"/>
    </a>
</div>

## How to get the example up and running
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
7. Add files to the local repository and commit the changes.
```
$ echo "Text" > example_file.txt
$ git add example_file.txt
$ git commit -m "Created example_file with Text as content."
[feature1 (root-commit) d694ee6] Created example_file with Text as content.
 1 file changed, 1 insertion(+)
 create mode 100644 example_file.txt
```
8. Push changes to user defined branch e.g. `feature1`.
```
$ git push --set-upstream origin feature1
Counting objects: 3, done.
Writing objects: 100% (3/3), 247 bytes | 247.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ../remote_repository/
 * [new branch]      feature1 -> feature1
Branch 'feature1' set up to track remote branch 'feature1' from 'origin'.
```

## Contributing
To get started with contributing to my GitHub repository, please contact me [Slack](https://join.slack.com/t/napi-friends/shared_invite/enQtNDg3OTg5NDc1NzUxLWU1MWNhNmY3ZTVmY2FkMDM1ODg1MWNlMDIyYTk1OTg4OThhYzgyNDc3ZmE5NzM1ZTM2ZDQwZGI0ZjU2M2JlNDU).
