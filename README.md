# Ubuntu 18.04 docker image with ROS Melodic and VNC Support for Windows

# Prerequisites 
* Windows 10 64-bit: Pro, Enterprise, or Education (Build 15063 or later).
* Hyper-V Virtualization enabled in BIOS

## How to install:
Install [Docker] for running ubuntu image.
Install [VcXsrv] to visualize ubuntu apps for OpenGL support.
Install [VncViewer] to visualize ubuntu desktop.
Open PowerShell and build the image using the following command (it might take some time to download 3 GB of data):
```sh
$ docker build -t ubuntu-vnc-melodic .
```


## How to run:
In PowerShell check the IP of your computer with **ipconfig** command.
Create a **DISPLAY** variable with:
```sh
Set-Variable -Name DISPLAY -value YOUR_IP:0.0
```
Run the container:
```sh
docker run -ti --rm -e DISPLAY=$DISPLAY -p 5901:5901 --name ubuntu-vnc-melodic ubuntu-vnc-melodic
```
After that we get access to a ubuntu terminal.

## How to show Ubuntu Desktop:
After starting the docker image run a VNC server from ubuntu terminal using command:
```sh
$ vncserver :1 -geometry 1280x800 -depth 24
```
The first run would require entering a password. The following message will show up:
```sh
You will require a password to access your desktops.

Password: [Enter password]
Verify: [Repeat password]
Would you like to enter a view-only password (y/n)? [Type n]
```
In order to close the created server type:
```sh
$ vncserver -kill :1
```

Launch **VNC Viewer** application on Windows to show a desktop:

* enter **127.0.0.1:5901** in the main window
* Enter a password and the ubuntu desktop would appear

![VNC](https://github.com/RafalStaszak/UbuntuMelodicDesktop/blob/master/vnc.PNG)


Launch **XLaunch** application on Windows to create an *X Desktop* instance (OpenGL support):

* select *Multiple windows* and set *Display number* to **-1**
* select *Start no client*
* select *Clipboard*, deselect *Native opengl* , select *Disable access control*

![Rviz](https://github.com/RafalStaszak/UbuntuMelodicDesktop/blob/master/rviz.PNG)

## How to work with Docker:
Docker is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called **containers**. Every container is created from an **image** instance which is a raw version of a software bundle. In such a setting containers may be described as actual running applications.

* **containers** are created from images
* the state of a container may be preserved by saving it into an **image**
* if container is not saved all the changes irreversibly disappear
* every container has an **ID** and optionally a name
* every image has an **ID** and a name in the *name:tag* format


To list existing docker images:

```sh
docker images
```

To list running docker containers:
```sh
docker container ls -a
```
Saving new changes in a container:
```sh
docker commit [name | container ID] [image name:tag]
```
Starting new shell with an already running container:
```sh
docker exec -it [name | container ID] /bin/bash
```

Stopping and removing container:
```sh
docker stop [name | container ID]
docker rm [name | container ID]
```
Removing image:
```sh
docker rmi [name | image ID]
```
![Commands](https://github.com/RafalStaszak/UbuntuMelodicDesktop/blob/master/commands.PNG)

   [Docker]: <https://docs.docker.com/docker-for-windows/>
   [VcXsrv]: <https://sourceforge.net/projects/vcxsrv/>
   [VncViewer]: <https://www.realvnc.com/en/connect/download/viewer/windows/>
