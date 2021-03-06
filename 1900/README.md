# 1900 The Container Lifecycle

In this lesson, we'll talk about how to create, start, and stop containers, as well as how to connect to an already running container. The GitHub repositories mentioned in this video are:

https://github.com/moby/moby

and

https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go

## Transcript

Everyone, welcome back to our docker quick start series and in this video we'll be discussing the container lifecycle. Now, for some reason, you're not following along in order. I want you to go back and watch our running containers video. That's because this is a continuation of that. In that video, we went in and we created our first container that we actually went into. It was called python Container inside of it, we created a hello world script and we went ahead and ran it. We ensure that python3  was working. The question is, what happens when we leave that container? You know, Is that container going to keep our script in? It will be able to start it. How do we ship with this? This is all part of our container Live cycle. 

So today we're going to be discussing how we go from that image to running the container to having that container stop to being able to restart it. And what do we do with the development that we've done inside of that container? 

So let's go ahead and get to that command and start getting our hands dirty. 

So we're going to kick things off by getting familiar with our environment. We'll do our docker images command that we're used to here just to see the images on our system. 

```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
<none>        <none>    f70b04ba7ac3   2 hours ago     198MB
ubuntu        16.04     9499db781771   5 weeks ago     131MB
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```

We can follow that up with our Docker container ls to see we have any containers currently running on this server. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

And after that, we can do docker container ls -a  to see if we had any containers previously running that are now in a stopped state. So we can see we are in a brand new clean environment. 

```
$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                       PORTS     NAMES
89c2806c55cd   f7            "/bin/bash"   33 minutes ago   Exited (127) 4 minutes ago             python-container
bc76fb087f98   hello-world   "/hello"      40 minutes ago   Exited (0) 40 minutes ago              boring_hoover
f7b22f1c91c9   hello-world   "/hello"      5 days ago       Exited (0) 5 days ago                  hungry_diffie
f935aaea254d   hello-world   "/hello"      5 days ago       Exited (0) 5 days ago                  intelligent_robinson
```

So why don't we go ahead and create a container so we can start learning about the life cycle In order to run this container will use our command docker container run. Then we use are similar flags that we've been using the  -i-t and then we will run our  ubuntu:16.04  image that hopefully we've become familiar with. 

```
$ docker container run -it ubuntu:16.04
```

Once we type enter we're in our container and we can see that with our docker container ls command. 

```
/#
```

So let's go ahead and jump to ***another terminal*** so that we can see that. 

```
$ docker container ls
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS     NAMES
85f4dda842c5   ubuntu:16.04   "/bin/bash"   3 minutes ago   Up 3 minutes             amazing_lichterman
```

We can see here that we have a container running and it's been named amazing_lichterman. 

Since we didn't provide a name, have you ever wondered where these names actually come from? Well, let me just jump over to another screen here, and I'll introduce you to the Moby Project (https://github.com/moby/moby and https://mobyproject.org). 

--

***What is Moby?***

Moby is an open framework created by Docker to assemble specialized container systems without reinventing the wheel. It provides a “lego set” of dozens of standard components and a framework for assembling them into custom platforms. At the core of Moby is a framework to assemble specialized container systems which provides components, tools, assemblies.

--

Now, the moby project is an open source project that was created by Docker to really help enable and accelerate software that is going to be containerized. Now, you can find this on their github (https://github.com/moby/moby ) and all week to the github in the description of this video. 

Now, I'm not going to spend a lot of time in this. This really is a deep dive concept. But since we haven't been naming our containers, I thought you might be interested in where the names were coming from. The moby project was intended to be able to provide a kind of a tool kit for Dockerized applications for containerized applications. And I might want to note that the relationship with Docker is that they are an open source component of docker but if you go into Moby, then you go into the packages file, then name generators named generators. 

https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go

Don't go. You'll begin to see some of the names that you may have become familiar with so to pull one from the string you make it admiring, adoring, affectionate. So it's more of an adjective. So it's more of a descriptive name. And if we scroll down a bit, we can see that the second name that will get pulled comes from the second list. You might get Alan or let's say, Austin, we even see the container name, which we pulled it as amazing_lichterman here on the screen. 

And if you have time, I'd really encourage that. You spend some time reading through this list, and it's just a great compilation of really influential people in the technical community. 

But for us, it's time for us to get back to our doctor containers. 

So what happens if we exit this container? Will the container continue to run? Will it go into a stop process once find out.

```
/# exit
```

And let's do our doctor container ls. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

We'll see if this container is no longer running. 

Let's go ahead and see if the container is in a stopped status. 

```
$ docker container ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                          PORTS     NAMES
85f4dda842c5   ubuntu:16.04   "/bin/bash"   21 minutes ago   Exited (0) About a minute ago             amazing_lichterman
89c2806c55cd   f7             "/bin/bash"   19 hours ago     Exited (127) 18 hours ago                 python-container
bc76fb087f98   hello-world    "/hello"      19 hours ago     Exited (0) 19 hours ago                   boring_hoover
f7b22f1c91c9   hello-world    "/hello"      6 days ago       Exited (0) 6 days ago                     hungry_diffie
f935aaea254d   hello-world    "/hello"      6 days ago       Exited (0) 6 days ago                     intelligent_robinson
```

All right, we see that the container is in fact, stopped. We can see amazing_lichterman there. 

Let's go ahead and clear our screen so we can see a little bit more of what we're doing. 

```
$ clear
```

So let's go ahead and do our doctor images so that we have a reference to which image that we used up on our screen that we can see and you can see that we use ubuntu 16.04 image with the command ```docker container run -it ubuntu:16.04```. 

```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
<none>        <none>    f70b04ba7ac3   20 hours ago    198MB
ubuntu        16.04     9499db781771   5 weeks ago     131MB
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```

*** WE ARE HERE ***

And with this did was it prepared our system in order for us to be able to instantiate a container to start a container from this image. 

```
$ docker container run -it ubuntu:16.04
/#
```

We went ahead and told it to run that ubuntu:16.04 for image. And when we clicked enter, we went from a just starting a container to an actual running container. 

Our container was up and running until we exited out of that container. 

```
/# exit
```

As soon as we exited out, it no longer needed to run the shell, which we required for it to use that been bashed shell that we see under command here (see vigorous_ritchie). 

```
$ docker container ls -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                      PORTS     NAMES
4fc9b64b73de   ubuntu:16.04   "/bin/bash"   2 minutes ago    Exited (0) 13 seconds ago             vigorous_ritchie
85f4dda842c5   ubuntu:16.04   "/bin/bash"   32 minutes ago   Exited (0) 12 minutes ago             amazing_lichterman
89c2806c55cd   f7             "/bin/bash"   19 hours ago     Exited (127) 19 hours ago             python-container
bc76fb087f98   hello-world    "/hello"      19 hours ago     Exited (0) 19 hours ago               boring_hoover
f7b22f1c91c9   hello-world    "/hello"      6 days ago       Exited (0) 6 days ago                 hungry_diffie
f935aaea254d   hello-world    "/hello"      6 days ago       Exited (0) 6 days ago                 intelligent_robinson
```

Um, and it wintered a stopped status. 

So we've kind of done our entire life cycle from Hey, we're going to start a container to running a container until we've stop the container. 

So what happens if we still want to use this container? 

You know, we've decided that we want to make a few more changes to our configuration. We want to test something new. Then we can use the command docker container start yield in what? To provide either the container id being that 4fc code or the container name being vigorous_ritchie. 

```
$ docker container run vigorous_ritchie
vigorous_ritchie
```

Well, if you do our doctor container ls we can see that we have that same container up and running vigorous_ritchie and destructed if he has been running for about a minute. 

```
$ docker container ls
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS              PORTS     NAMES
4fc9b64b73de   ubuntu:16.04   "/bin/bash"   8 minutes ago   Up About a minute             vigorous_ritchie
```

Basically bringing everything full circle. We started our container with a docker container run. Once we hit Enter and told it that we wanted it to run that ubuntu 16.04. Our container was up and running we then exited out of our container which caused it to stop. And then we asked it to start that same container again. So we're back in that same cycle. 

Go ahead and clear our screen for a little bit more room. 

```
$ clear
```

A docker container at ls will help us find our I.D. and name for container and I know, it seems we're being a bit repetitive, but really doing repetitive tasks really does help you learn something new. 

```
$ docker container ls
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS         PORTS     NAMES
4fc9b64b73de   ubuntu:16.04   "/bin/bash"   13 minutes ago   Up 6 minutes             vigorous_ritchie
```

So what happens if I want to be able to attach to this container again, though. 

Well I can do a ```docker attach``` and I could use the name vigorous_ritchie or just the I.D. enough id's to differentiate it from any other running container. 

So 4f would be about all that I actually need. 

```
$ docker attach 4f [ENTER]
/#
/#
```

Now I've accidentally entered an Enter here, so that's why we have our double prompt. But I could do something like ls. 

```
/# ls
bin  etc  lib64 opt  run  sys var
boot home media proc sbin tmp
dev  lib  mnt   root srv  usr
```

And you can see that our environment is indeed up and running we can exit back out of this container. 

```
/# exit
```

And, as expected, we could docker container ls and see that this environment or this container is no longer running. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

Let's docker container ls -a and we can see that once again, it's in a stop status. 

```
$ docker container ls -a
CONTAINER ID   IMAGE          COMMAND       CREATED             STATUS                          PORTS     NAMES
4fc9b64b73de   ubuntu:16.04   "/bin/bash"   29 minutes ago      Exited (0) About a minute ago             vigorous_ritchie
85f4dda842c5   ubuntu:16.04   "/bin/bash"   About an hour ago   Exited (0) 40 minutes ago                 amazing_lichterman
89c2806c55cd   f7             "/bin/bash"   19 hours ago        Exited (127) 19 hours ago                 python-container
bc76fb087f98   hello-world    "/hello"      20 hours ago        Exited (0) 20 hours ago                   boring_hoover
f7b22f1c91c9   hello-world    "/hello"      6 days ago          Exited (0) 6 days ago                     hungry_diffie
f935aaea254d   hello-world    "/hello"      6 days ago          Exited (0) 6 days ago                     intelligent_robinson
```

So hopefully you now have a better understanding of the container life cycle. And I hope that part of you is wondering. OK, so how do we take our script and actually have it run within our environment? That's the questions that we'll get to in the next video. 

So go ahead and close this one out and continue on with your journey.
