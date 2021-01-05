# 1800 Running Containers

In this video, we will learn how to create a container and connect to it so we can see some real-world use cases for Docker. This video will lay the foundation for upcoming lessons on the container lifecycle.

## Transcript

Hi everyone. We're back with our Docker Quick Start course. And now we're gonna discuss actually running containers. Now you're saying L You've been running containers this whole time, All right? I did cheat a little bit by running container to show you how to tell whether your environment was up and running. I kind of showed you are hello world image by running that container. Don't worry about it. There's a lot more to running containers. In fact, we don't have to just run an image that spins up, puts out some output and then the container closes. We're gonna be creating containers that are meant to last for a little bit. 

Now, don't get me wrong. Containers are meant to be ephemeral in nature. This means that they are meant to kind of just come up, do the job that they need to do and go away. 

However, when you're developing, at times, you need these containers to last a little bit longer so that you're able to tell whether your code is working, how your application is being maintained. That's what we're gonna be covering today. 

We're gonna be creating a container from our ubuntu image. We're going to be going into it and exploring the environments a little bit, seeing how we might use it in a testing environment and all kind of delve into a little bit of some groundwork that I've been laying for you. 

You see, this whole time we've been using the command docker run, but Docker has been growing. There's a lot more to the product, so I'll introduce you to the command docker container run and discuss a little bit about why that change was made. So I'm gonna go ahead and disappear so we can get to the real meat of this subject. And we can see what environment were logged into by doing our docker images and you'll see that we have two images. These are the ones that we used in that Docker file video. 

```
$docker images
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE
<none>        <none>    f70b04ba7ac3   About an hour ago   198MB
ubuntu        16.04     9499db781771   5 weeks ago         131MB
hello-world   latest    bf756fb1ae65   12 months ago       13.3kB
```

Now, please note that we haven't added a name or repositories to it because we'll be doing that in a subsequent video. 

We're building a story here together. 

Another thing to know is that it's time for us to build on the command is that we've been learning. Now we've used that docker images command throughout the course will be introduced. A new command to you. And that's Docker image ls 

```
$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE
<none>        <none>    f70b04ba7ac3   About an hour ago   198MB
ubuntu        16.04     9499db781771   5 weeks ago         131MB
hello-world   latest    bf756fb1ae65   12 months ago       13.3kB
```

As you can see, it does everything that the command above does Dr Images. However, as the community has grown as the Docker community has grown, they've moved towards using commands that really give you information about what you're interacting with. It's very similar to when I built this image. I did that app get installed. Python three. Even though all you really needed to do was apt Install Python three. The one command, maybe legacy. It's still available and still works. So why have I spent all this time teaching you that Dr Images Command? Why didn't I start out with the doctor image? L s command. That's because as information comes out blawg post documentation information that you can find throughout the Internet to give you explanations on how to troubleshoot things. We don't really tend to go back and update our documentation. So is your reading older block post? Even at the docker documentation itself, you'll still find information on Docker Images. I think that by teaching you that legacy command what it does, the information that it gives you it's not too much of a leap for you to pick up the newer command. 

The same is the case with our Docker run command. In order to create containers. We've been doing the doctor run, and we've been using that hello world image. However, the updated command is Docker container Run 

```
$ docker container run hello-world
```

Now we didn't have that in our system. It went ahead and pull that down. Here. You get it. We have the same image we've been working with. We can do that docker image ls and we can see that we now have hello world as well as our previous two images. But running containers is so much more than that simple hello world image. You know, that one was really written just to give us an output. When that container is instantiated from our hello world image. But what if we're working on development like I talked about being able to create this image here? 

```
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE
<none>        <none>    f70b04ba7ac3   About an hour ago   198MB
```

Let's go ahead and instantiate a container from our unnamed image. So that's going to be docker container Run. I'm gonna go ahead and clear my screen first that you guys are. If you're looking at this through a tablet or cell phone, are trying to focus at the very bottom of your screen. All right, so let me get my images one more time. 

```
$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE
<none>        <none>    f70b04ba7ac3   About an hour ago   198MB
ubuntu        16.04     9499db781771   5 weeks ago         131MB
hello-world   latest    bf756fb1ae65   12 months ago       13.3kB
```

So I have that i'd now docker container run. 

There are a couple of flags which will be using here dash I for interactive dash t So that we can allocate a sudo of t t y. I'll go ahead and use the dash dash, name, flag so we can begin to learn how to name or containers. And I'm not very creative. So will simply go with python container as the name. Now I could do the entire image I d However, it only needs enough information to be able to distinguish it from the other images. So simply a f7 will work as this doesn't have any other conflicts. 

```
$ docker container run -it --name python-container f7 
```

Now we notice that my prompt has changed. That's because I am, in fact, inside of that container. 

```
root@89c2806c55cd:/#
```

So let's go ahead and see what version of Linux we're running. Well, we should expect that we should be running on that A boon to 16 0 for image, just as we suspected. 

```
$/# cat /etc/issue
Ubuntu 16.04.7 LTS \n \l
```

Well, what about Python? Is it actually installed on this system? So if this build occurred the way that we told it to. We should also have access to a Python three and go ahead and just issue the Command Python three and you'll see that I dropped down into the interactive command line for Python3. 

```
$/# python3
Python 3.5.2 (default, Oct  7 2020, 17:19:02) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

We go ahead and exit, though, because we're focused on the container, not on Python and as a developer.

```
>>> exit() 
```

Let's say that I wanted to create a script, too, just to ensure that it would work in this environment. 

I could exit out of this container and push a script into the container or I can develop in here. 

Now I can use my command vim and then my script name. 

```
$/# vim hello-world.py
bash: vim: command not found
```

However, you'll notice that vim is not installed in this environment, and some of you may be saying Okay, so we need to update that on boarding image to contain them. 

Do we really some of my developers, maybe using Nano, they may be using something else. Really, that's up to them, and we'll show you later how we can pull scripts into our container environment without needing to be able to write them in here. 

But for now, I'll go ahead and install it just for demonstration purposes? No, This is for demonstration and development purposes and not best practices on how to use a container. 

```
$/# apt install vim
```

Let's go ahead and create that quick hello world script I might do. 

```
$/# vim hello-world.py
```

This isn't a coding class. We're going to keep it simple here. 

```
print("Hello World!")
````
hello-world.py

I can go ahead and chmod my file.  

```
$/# chmod +x hello-world.py
```

Oops python3. There we go.

```
$/# python3 hello-world.py
Hello World!
```

Now, that was kind of Quick and Dirty Python, but we know that my script can work inside of this containerized environment. 

```
$/# exit
$
```

Now, hopefully this example has provided you with kind of view on why we would be using these containerized environments. Let's say that we had someone who was perhaps using Scientific Linux or maybe even a Red Hat Linux and they were developing on Python 2 sharing this image and allowing them to instantiate a container for a minute and be able to run a script on python three. Do some development or some testing really wouldn't be a big deal. It be quite simple for them to do that. We just did it. 

Okay, everyone, that hopefully you now have a better understanding of how to interact at how to run your containers. 

Now, I did say that containers are ephemeral in nature. So in the next video, we're gonna take the time to understand our container lifecycle. Being able to understand really what we mean when we say that containers are intended to be ephemeral. 

Until then, though, you can go ahead and close out this video and continue on with your journey.
