# 1400 Installation and Configuration: Linux - Part 2

In this video, we will revisit the Linux installation process, as there is always more than one way to perform a task on Linux. Scripts for this installation can be found at:

[https://get.docker.com](https://get.docker.com)

and

[https://github.com/docker/docker-install](https://github.com/docker/docker-install)

## Transcript

Hey everyone, It's Ell Marquez again. And if you're following along with our docker Quick start guide, I'm sure at this point you're wondering. Is she telling me the full truth? Do we really need to go through this extended docker install every time I need a new environment? All right, you got me. That's not the only way to install Docker, but that tends to be the truth with anything in Linux, right? There are multiple ways to do something. So as you can imagine, many system admins and other developers got tired of going through this process every time. So now that you've gone through, the longer more intel, the process of installing Docker let me show you how to do it through a scripted method. 

```
$ wget -qO- https://get.docker.com |sh
```

So here we're logged into our cloud server and you can see that we're gonna be using the W get command in order to pull the script onto our server so that we can install Docker. This script is provided by Docker at get.docker.com 

*** WE ARE HERE ***

However, you don't blindly want to run scripts on your server. Of course, you want to want to see what's actually located or composed of this script. So let's go ahead and go to that URL and you can see here what commands this script is going to be running. And also states that if you want to make sure to verify the contents of the script, you can do so on Docker GitHub. 

= script content goes here =

However, as this is a quick start, not a deep dive. Let's go ahead and go back to our command line and see the script install. 

```
# Executing docker install script, commit: 3d8fe77c2c46c5b7571f94b42793905e5b3e42e4
Warning: the "docker" command appears to already exist on this system.

If you already have Docker installed, this script can cause trouble, which is
why we're displaying this warning and provide the opportunity to cancel the
installation.

If you installed the current Docker package using this script and are using it
again to update Docker, you can safely ignore this message.

You may press Ctrl+C now to abort this script.
+ sleep 20
+ sudo -E sh -c 'yum install -y -q yum-utils'
```

Now, I'm gonna go ahead and jump in here for a second and do a little truth in advertising maybe that's because sometimes this GPG section really does take a while to happen. And I don't want you just sitting here staring at this screen. So I'm gonna go ahead and edit it down through the magic of video editing. So you may need to pause this video and allow the installation to continue. But once we are up and running and installed, it runs just like our other Docker environment we'll go ahead and add our cloud user (note: this is specific to Linux Academy) to the docker groups so that we can use those privileged docker commands. 

```
$ sudo usermod -aG docker cloud_user
```

But we seem to have a problem here. 

```

```

It says the docker is unable to connect to our daemon. That's because though we did do our install process, we've not gone ahead and enabled as well as started the docker daemon on this system. So do so. But remember to use your sudo command as this is a privileged action to be able to run a service on a server. Then once we've done so, though, we still can't seem to use those docker. We still can't seem to use those Docker commands and that's because we'll need to log out and log back into our server to ensure that our permissions have been read by the system. Let's go ahead and do that. And once we've done so, we can go ahead and use commands like Docker version, and we're ready to go. So now you know how to install docker on Linux in two ways. One being the more extended version, but I really would encourage you to take the time and learn that before, just automatically opting to use a scripted version. Go ahead and close out this video and we can continue on learning more about Docker. 
