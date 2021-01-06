# 2000 Image and Container Management

We now know how to pull and install images and instantiate containers. Removing them is equally important, but there are some caveats. Let's talk about what we need to know!

## Transcript

Hey everyone,  It's El Marquez with our docker Quick start series in this video. I'm going to try to keep it short and to the point. 

Now it's labeled container and image management. So that's what you're going to be learning in this video. You're going to be learning what to do with all the images that you no longer need. How to tell when a container is still running? What containers are currently stopped, but still taking resources on our bucks. So let's go ahead and get to it and get to cleaning up our environment. So our first move as usual, is going to be to get used to our environment. So let's do our docker container LS to see what containers we have running on this system. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

You see that we currently don't have anything. 

So let's do that, docker container ls -a and we could see that I have two containers had created another one for testing purposes earlier. 

```
$ docker container ls -a
CONTAINER ID   IMAGE          COMMAND       CREATED        STATUS                      PORTS     NAMES
4fc9b64b73de   ubuntu:16.04   "/bin/bash"   2 hours ago    Exited (0) 2 hours ago                vigorous_ritchie
85f4dda842c5   ubuntu:16.04   "/bin/bash"   3 hours ago    Exited (0) 2 hours ago                amazing_lichterman
89c2806c55cd   f7             "/bin/bash"   21 hours ago   Exited (127) 21 hours ago             python-container
bc76fb087f98   hello-world    "/hello"      21 hours ago   Exited (0) 21 hours ago               boring_hoover
f7b22f1c91c9   hello-world    "/hello"      6 days ago     Exited (0) 6 days ago                 hungry_diffie
f935aaea254d   hello-world    "/hello"      6 days ago     Exited (0) 6 days ago                 intelligent_robinson
```

And look at our docker images and we can see that our three (here more than three) usual images. 

```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
<none>        <none>    f70b04ba7ac3   23 hours ago    198MB
ubuntu        16.04     9499db781771   5 weeks ago     131MB
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```

So what if I'm done with this? At this point, I no longer need these containers. Well, in order to remove them, it's a simple command docker container RM for remove. Then we go ahead and we put in the container. ID and I could just push enter, and it will remove that container. 

```
$ docker container rm 4fc9b64b73de
4fc9b64b73de
```

Let's say that I want to go ahead and remove both containers. Then it's a simple doctor container RM again. And this time I could use the ID. Or as I've gotten attached to using the name amazing_lichterman, I can go ahead and use that. Let's click enter and amazing_lichterman is no longer with us. 

```
$ docker container rm amazing_lichterman
amazing_lichterman
```

I could have also removed them both at the same time with docker Container RM and listed both the container ID, the name or a combination thereof. Right? 

```
$ docker container rm boring_hoover f7b22f1c91c9
boring_hoover
f7b22f1c91c9
```

Let's clear our screen and we can do a docker container ls -a and we can see that neither of these containers is available on our system anymore.

```
$ clear
$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND       CREATED        STATUS                      PORTS     NAMES
89c2806c55cd   f7            "/bin/bash"   21 hours ago   Exited (127) 21 hours ago             python-container
f935aaea254d   hello-world   "/hello"      6 days ago     Exited (0) 6 days ago                 intelligent_robinson
```

Alright, let's do our images command in order to be able to see what images are on this box, and we can see the same three. 

```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
<none>        <none>    f70b04ba7ac3   23 hours ago    198MB
ubuntu        16.04     9499db781771   5 weeks ago     131MB
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```

But you know what I'm done with hello-world. We've used that one enough times. Let's go ahead and remove from our box. The command is ***docker rmi*** That's remove image, and the image is no longer on our box. 

```
$ docker rmi bf756fb1ae65
Untagged: hello-world:latest
Untagged: hello-world@sha256:1a523af650137b8accdaed439c17d684df61ee4d74feac151b5b337bd29e7eec
Deleted: sha256:bf756fb1ae65adf866bd8c456593cd24beb6a0a061dedf42b26a993176745f6b
Deleted: sha256:9c27e219663c25e0f28493790cc0b88bc973ba3b1686355f221c38a36978ac63
```

I could go through and remove the remainder of these images. However, if you recall the image which we created, which is currently on tag, we really haven't saved anywhere outside of our docker file. So what if I wanted to save it? Well, in order to do so, I could simply push up this image into the docker hub. So let me clear out my screen here so that we can see a little bit better. 

```
$ clear
```

And I've pulled up our lucid chart here in the corner. For those of you that may be visual learners. So the first thing I'm going to do is I'm going to log into my docker hub account with a command docker login.  

```
docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: wvanheemstra [ENTER]
Password: ***** [ENTER]
WARNING! Your password will be stored unencrypted in /home/cloud_user/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

Now we want to use the ID that we created previously in the series in order to create our docker hub account. 

Which for me is ellopunk (here: wvanheemstra). 

Same password is we used in our docker hub, and you can see we have logged in successfully. 

Let's go ahead and list out our docker images so that I can grab the id for the image that we created. 

```
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
<none>       <none>    f70b04ba7ac3   23 hours ago   198MB
ubuntu       16.04     9499db781771   5 weeks ago    131MB
```

So we're going to use the command, docker tag, and then we'll give it the id of the image that we created. 

So that's going to be that f70b04ba7ac3 number that I just copied that I'm going to let it know that I wanted to go into my area of the docker hub. So you can think of me as perhaps the distribution that is giving out this image. 

So I'll be using ellopunk (here: wvanheemstra). Please use your own here. Now my image is going to be tagged as an onboarding v1 image later on, who knows? 

```
$ docker tag f70b04ba7ac3 wvanheemstra/onboarding:v1
$
```

Maybe I'll do some updates and I'll have onboarding version 2. 

I will note that there is also another version of this command, which would be your docker image tag, it works exactly the same. 

So let's do our docker images or you can do a docker image ls if that's better for you, and that'll show you that our image tags have indeed been updated. 

```
$ docker images
REPOSITORY                TAG       IMAGE ID       CREATED        SIZE
wvanheemstra/onboarding   v1        f70b04ba7ac3   23 hours ago   198MB
ubuntu                    16.04     9499db781771   5 weeks ago    131MB
```

So let's go ahead and push this up to the docker hub. So let's do docker push. ellopunk (here: wvanheemstra). is going to be mine. 

***NOTE***: Create a repository with the name "onboarding" under the account "wvanheemstra" on the Docker Hub first, before proceeding.

Make sure to put your user name in here. We'll do a backslash and I'm going to want to create a repository for this image specifically for my onboarding image. So I'll just call it onboarding. 

```
$ docker push wvanheemstra/onboarding:v1
The push refers to repository [docker.io/wvanheemstra/onboarding]
7ce6b5f3a551: Pushed 
29e7b0a8f4d7: Pushed 
1a1a19626b20: Mounted from library/ubuntu 
5b7dc8292d9b: Mounted from library/ubuntu 
bbc674332e2e: Mounted from library/ubuntu 
da2785b7bb16: Mounted from library/ubuntu 
v1: digest: sha256:dbcb7ee1ff2630b5e058be288de63d219d4472125ac7926e99806b42a2ef7cec size: 1574
```

It says here this push refers to the repository docker.io/ellopunk/onboarding (here: https://hub.docker.com/repository/docker/wvanheemstra/onboarding). 

We'll visit that in the docker hub in just a bit, but I do want to take a moment here and look at what you're seeing on your screen. What you see is there were two image layers that were pushed to the Docker hub. However four came from your ubuntu library. Do you recall when we looked at that, ubuntu image. It had four image layers. Those are the ones being copied from the ubuntu to library. After all, there's no reason to push him up if they're already there. right. And our two changes are what are being pushed up to our repository. You don't recall what these changes are. Let's go ahead and cat out our docker files so we can see what changes we made. 

```
$ cat onboarding/dockerfile
FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y python3
```

So you can see that we started out with ubuntu 16.04. That's going be your four mounted layers. 

Then we did our added our label that didn't create a layer because it's just a change in metadata (here; skipped). 

Then we did our ```RUN apt-get update```. That's going to be one of your layers pushed. 

And then we did our ```RUN apt-get install -y python3``` which is going to be the other layer that was pushed. 

Let's jump over and take a look at this in the docker hub. 

```
https://hub.docker.com/repository/docker/wvanheemstra/onboarding
```

So here I'm in the docker hub. You can see that I'm logged in as the ellopunk (here: wvanheemstra) user. 

I now have an onboarding repository with my v1 image. 

If I want to push up additional tags for this repository. Let's say perhaps a v2 it even lets me know how to do that. 

```
docker push wvanheemstra/onboarding:tagname
```

Now that I have my image in the safe place, I can get to erasing images. 

But let me show you one last thing. 

When I tried to erase these images, I tried to erase the ubuntu image before I deleted that onboarding image and I ran into an issue. 

```
docker rmi 9499db781771 f70b04ba7ac3
Error response from daemon: conflict: unable to delete 9499db781771 (cannot be forced) - image has dependent child images
Error response from daemon: conflict: unable to delete f70b04ba7ac3 (must be forced) - image is being used by stopped container 89c2806c55cd
```

The issue being that, the onboarding image depends on that ubuntu image for those four image layers. So while I still have it on my system, it wouldn't really make sense to delete it because I'd be deleting a portion of my image. 

*** WE ARE HERE ***

Now that we've deleted that onboarding image, we can go ahead and delete our ubuntu image. Well, what happens when I'm ready to create that v2 what If I want to have v1 as my inspiration. 

No problem all I need to do is a docker pull. Tell it what repository it's going ellopunk. I want my onboarding v1 image. And there you go our onboarding image is back on our system. 

So hopefully all of you did not find that too complicated. The great thing about docker is that their help pages really do show us everything that we need to know, but for now, hopefully you feel a little bit more comfortable working around your environment and being able to clean up images and containers when they're no longer needed. 

Go ahead and close out this video and we'll continue on with our journey
