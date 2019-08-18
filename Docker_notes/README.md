<img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fd3nmt5vlzunoa1.cloudfront.net%2Fphpstorm%2Ffiles%2F2015%2F10%2Flarge_v-trans.png&f=1" alt="Docker logo" height="42px" width="42px" align="left"><br>

# Docker Toolbox Notes
<div>
    <a href="https://github.com/NaPiZip/Tipps-and-tricks">
        <img src="https://img.shields.io/badge/Document%20Version-0.0.1-green.svg"/>
    </a>
    <a href="https://www.microsoft.com">
        <img src="https://img.shields.io/badge/Windows%2010%20x64-10.0.17134%20Build%2017134-blue.svg"/>
    </a>
    <a href="https://docs.docker.com/toolbox/toolbox_install_windows/">
        <img src="https://img.shields.io/badge/Docker%20Toolbox-17.05.0--ce%20Build%2089658be-blue.svg"/>
    </a>
</div>

## How to use Docker Volume
Docker offers the option to mount a directory into a container with the volume flag before running it. The following example shows how start the `jupyter/minimal-notebook` container in interactive, pseudo tty mode `-it` while mounting volume `E:/080_Github` into directory `/home/jovyan/work`.

```
$ docker image ls
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
jupyter/minimal-notebook   latest              6bf2cb6cc671        3 days ago          2.72GB

$ docker run -it -p 80:8888 -v /e/080_Github/:/home/jovyan/work jupyter/minimal-notebook
Executing the command: jupyter notebook
[I 04:03:11.564 NotebookApp] Writing notebook server cookie secret to /home/jovyan/.local/share/jupyter/runtime/notebook_cookie_secret
[I 04:03:12.230 NotebookApp] JupyterLab extension loaded from /opt/conda/lib/python3.7/site-packages/jupyterlab
[I 04:03:12.230 NotebookApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
[I 04:03:12.237 NotebookApp] Serving notebooks from local directory: /home/jovyan
```

## Purging All Unused or Dangling Images, Containers, Volumes, and Networks
Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are dangling (not associated with a container), link can be found [here](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes):
```
$ docker system prune
WARNING! This will remove:
        - all stopped containers
        - all volumes not used by at least one container
        - all networks not used by at least one container
        - all dangling images
Are you sure you want to continue? [y/N] y
Deleted Containers:
dddfae23373bfe21c30ba180c947b0e0825422131a05a04713c1a015f6e82596
44163b9b2a272aa6f37d2d88aae4ccbb743b4015f57e84ffd0418443925199c6
...
```

## Cleaning dangling Containers
It sometimes happens that container images are dangling, meaning a build failed and they are not usable. In this case a clean up is needed in order to restore space.

```
$ docker rm $(docker ps -a -q)
690c7e56888f
13d4ef547b5a
079bc4796968
8ddea7297dcf
ec67b4c6f861
6d02f18cbb9e
a79fbc753761
```
## How to attach a bash into a running Container
It is helpful form time to time to debug a running container, the following steps describe the procedure.

1. Open a new Docker Quickstart Terminal.
2. Locate the container of interest.
```
$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS                  NAMES
ab05adb76f7e        jupyter/minimal-notebook   "tini -g -- start-..."   3 minutes ago       Up 2 minutes        0.0.0.0:80->8888/tcp   jolly_wescoff
```
3. Run the following command with the specified container id and the `/bin/bash` application at the end.
```
$ docker exec -it ab05adb76f7e /bin/bash
jovyan@ab05adb76f7e:~$
```

## Regenerate Certificates
Sometimes docker gets stuck and wont run, it could eb helpful to recreate certificates as follow:

```
$ docker-machine regenerate-certs -f default
Regenerating TLS certificates
Waiting for SSH to be available...
Detecting the provisioner...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
```
## Creating a new VM
The following command creates a new virtual machine called `newVM` with 4Gb of storage.
```
docker-machine create -d virtualbox --virtualbox-disk-size "40000" newVM
```

## Mounting Windows Directories in Containers
This is a description on how to mount additional directories within our Docker container that are outside of the users directory. To mount additional directories, you need to add the directory as a shared folder within Virtualbox and then enable long file paths and symlinks. Once the Virtualbox shared folders are setup, you need to mount the directories within the docker machine so that they are available to the containers, see [digitaldrummerj](https://digitaldrummerj.me/docker-windows-mounting-directories/).

1. Stop all running Docker container.<br>
```
$ docker stop [Container ID]
```
2. Stop the Docker machine, it is usually `default`.
```
$ docker-machine stop [machine name]   
```
3. Navigate to the Virtualbox directory.
```
$ cd "C:\Program Files\Oracle\VirtualBox"
```
4. Run the following command in order to add e.g. `E:080_Github/` drive.<br>
```
VBoxManage.exe sharedfolder add default --name "e/080_Github" --hostpath \\?\e:\080_Github" --automount
VBoxManage.exe setextradata default VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root 1
VBoxManage.exe setextradata default VBoxInternal2/SharedFoldersEnableSymlinksCreate/e//080_Github 1
```
5. Open the Docker Quickstart Terminal.
6. SSH into the Docker machine, e.g. default.
```
$ docker-machine ssh default
```
7. Check if the links exist if not create them.
```
$ sudo mkdir --parents /e/080_Github
$ sudo mount -t vboxsf e/080_Github /e/080_Github/
```

## Displaying logging information continuously
This section describes how to display the logging information of an detached running container to stdout.

1. Identify running container.
```
$ docker ps
```
2. Run logging command with the `-f` follow log output flag.
```
$ docker logs [Container ID] -f
```

## Contributing
To get started with contributing to my GitHub repository, please contact me [Slack](https://join.slack.com/t/napi-friends/shared_invite/enQtNDg3OTg5NDc1NzUxLWU1MWNhNmY3ZTVmY2FkMDM1ODg1MWNlMDIyYTk1OTg4OThhYzgyNDc3ZmE5NzM1ZTM2ZDQwZGI0ZjU2M2JlNDU).
