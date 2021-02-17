# 1300 Installation and Configuration: Linux — Part 1

In this video, we will discuss how to install Docker in a Linux environment. We're going to install Docker on a CentOS server, but the steps for installation on Ubuntu are essentially the same. For Ubuntu installation instructions, go here:

https://github.com/linuxacademy/content-container-essentials-101presentation/blob/master/Docker_Install_Ubuntu.md

Note: Install container-selinux before installing docker-ce. You can do so by looking up the correct package http://mirror.centos.org/centos/7/extras/x86_64/Packages then installing it on the system:

```sudo yum install http://mirror.centos.org/centos/7/extras/x86_64/Packages/container-selinux-2.107-3.el7.noarch.rpm```

## Transcript

Hey, everyone, we're back with our Docker QuickStart class, and the first thing that we're going to do is we're going to install Docker. Now, today we're going to be installing it on a Linux CentOS Cloud Server that's available here for you to use at Linux Academy. However, you really can install in any environment whether that be your Linux desktop or even Ubuntu. Now I'll have a guide written up on how to install Docker through Ubuntu and all insured to share that in the link of the description of this video. So regardless of what operating system you're going to be using, you really going to follow the same format. Now, I'm going to do these videos really focused on the command line and at our diagram. However, I am going to pop up every once in a while and explain important concepts to you. So with that go ahead and spit up a cloud server and follow along. 

So the first thing that we're going to be doing is we're going to be SSHing into one of our Cloud servers provided here at Linux Academy will be using the cloud user. Now, as the demo gods go, I always seem to get the password wrong the first time, so we're just going to go ahead and clear that away and let's give a shot at looking to see what operating system were using that. 

```$ cat /etc/redhat-release```

```CentOS Linux release 7.8.2003 (Core)```

+++

***NOTE***: For CentOS 8 follow the instruction at https://linuxconfig.org/how-to-install-docker-in-rhel-8

Red Hat Enterprise Linux 8 does not support Docker: on this distribution it has been replaced by Red Hat own tools like buildah and podman, which are compatible with Docker but don't need a server/client architecture to run. Using native tools, where possible, is always the recommended way to go, but for a reason or another you may still want to install the original Docker. In this tutorial, we saw how it is possible to install Docker CE on Rhel8, by using the official Docker repository for CentOS7, which is a 100% compatible clone.

This is not an ideal solution, and as we saw, at the moment, some workarounds are needed to make Docker work on RHEL8.

+++

So, for today's example, we're going to be installing on CentOS as mentioned before, there will also be a guide on how to install through Ubuntu. One of the first things that were going to do, though, is ensure that we have all of the packages that we needed in order to be able to install Docker, this is going to include your yum-utils package device mapper, persistent data as well as LVM2. 

```$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2```

As you can see if you're using a Linux Academy Cloud server, these packages have already been installed. However, it never hurts to ensure that they have been installed before proceeding. The next thing that we're going to do is we're going to add the repository that we need in order to install the version of Docker that we're going to be using. 

```$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo```

```
Loaded plugins: fastestmirror
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
```

Now, the URL, in order to download Docker, always makes me laugh because it's very intuitive. You just go to download.docker.com/ the operating system, which you're going to be using, which is Linux the version of that operating system centos/docker- CE for Community Edition and EE for the enterprise edition.repo were installing that repo. 

Once we have that repository configured, all we'll need to do is do a Yum Install Docker-CE once again for the Community Edition and -EE for the Enterprise Edition. 

```$ yum install docker-ce```

```
Loaded plugins: fastestmirror
You need to be root to perform this command.
```

```$ sudo !!```

```
sudo yum install docker-ce
...
```

Now it's always good to remember that this is a privileged command as we start going through our install process, the first thing that we're in a pause on is asking whether we want to install Docker CE as well as container as SE Linux. 

```
...
Install  1 Package (+7 Dependent packages)

Total download size: 102 M
Installed size: 423 M
Is this ok [y/d/N]:
```

Now, if I know some of you that are following along, you just added a -y flag and let this go through, but I think when you're first installing something, it's important to pause and see what is it that you're actually installing. If you're unfamiliar with it, Container SE Linux are simply the policies for container run time within a Red Hat environment. So I could be a Red Hat. You're CentOS for door environment. We'll go ahead and say yes here. 

```
Is this ok [y/d/N]: y
```

Then we'll move on to our GPG keys. 

Now, as we did not already have Dockers GPG keys on our system and went ahead and retrieve that key, and now it's importing it and then asking us, you know, are you sure that this is the correct GPG key? If for some reason we were not, we could go ahead and check our Docker documentation to ensure that it is so we can go ahead and say yes. 

```
Retrieving key from https://download.docker.com/linux/centos/gpg
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
```

So as it installed these packages primarily your container SE Linux policies, it is going to take a bit of time. So we through the magic of visual editing, we can go ahead and shorten that time for you. 

```
...
Installed:
  docker-ce.x86_64 3:20.10.1-3.el7                                                                     

Dependency Installed:
  container-selinux.noarch 2:2.119.2-1.911c772.el7_8  containerd.io.x86_64 0:1.4.3-3.1.el7             
  docker-ce-cli.x86_64 1:20.10.1-3.el7                docker-ce-rootless-extras.x86_64 0:20.10.1-3.el7 
  fuse-overlayfs.x86_64 0:0.7.2-6.el7_8               fuse3-libs.x86_64 0:3.6.1-4.el7                  
  slirp4netns.x86_64 0:0.4.3-4.el7_8                 

Complete!
```

And now our packages are installed, so let's go ahead and enable Docker, as well as starting Docker. 

```
$ sudo systemctl enable docker
```

```
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
```

```
$ sudo systemctl start docker
```

Now, at this point, docker is installed, enabled and started on our system. This means we can go ahead and use it, right? Well, not quite. 

Let's go ahead and clear the screen so I can show you what I'm talking about. 

```
$ clear
```

Now I'm going to be using the command sudo and we'll address why in just a moment we're going to do sudo docker run and the container that we're going to be running is called hello world. 

```
$ sudo docker run hello-world
```

```
Unable to find image 'hello-world:latest' locally
```

Now we're unable to find this in our system, as this is a brand new docker install. So it's going to go ahead and pull that from the docker library, and once this has been completed, it'll go ahead and run. 

```
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:1a523af650137b8accdaed439c17d684df61ee4d74feac151b5b337bd29e7eec
Status: Downloaded newer image for hello-world:latest
...
Hello from Docker!
...
```

And as you can see, this container is simply a small docker image that shows that your installation has worked correctly. The fact that this container ran proves that the docker client was able to contact the Docker daemon, the Docker daemon was able to pull the hello world image from that docker hub, and the Docker daemon was able to create a new container from that image, which produced the output that you're seeing on your screen now. 

```
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

The Docker daemon was able to screen that output to the docker client, which is what sent it to your terminal. This is a great image to show how exactly the docker image ran, and we are going to be digging deeper into this process. 

But the reason that I said you know that we're going to go back to that sudo to command is the fact that I ran that as a privileged user. What would happen if I tried to run this command as simply our cloud user? Let's go ahead and try that by clearing our screen. 

```
$ clear
```

So we do our docker run hello world and suddenly we have permission denied. 

```
$ docker run hello-world
```

```
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

That's because our cloud user (note: this is specific for Linux Academy) does not have the permissions to be able to use Docker. And so we can modify this or correct this issue by adding our cloud user to our docker group. 

```
$ sudo usermod -a -G docker cloud_user
```

Now, although there are ways to get around needing to log out and log back in when you make these fundamental changes in a Linux environment, it really is best practices just to log out of that user and log back in, in order to ensure that all the environmental variables and changes are read. 

```
$ exit
```

Now that that's a card, let's go ahead and try that command one more time without sudo. 

```
$ docker run hello-world
```

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

And I will have you noticed one difference, when I ran this command were no longer needing to pull that image from the docker hub because the docker, because the image already exists on our system. 

Okay, everyone as simple was that you are now up and running with your own docker environment. Now, technically, I guess we did cheat a bit because we did run our first container. So in order to understand how you did that and to continue using your environment, let's go ahead and close out this video and continue on with our journey. 
