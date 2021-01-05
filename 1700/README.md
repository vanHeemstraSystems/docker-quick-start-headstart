# 1700 The Dockerfile

In this video, we will discuss Dockerfiles and create the "Get Started Image" that we discussed in the Docker Images video lesson. Dockerfile best practices can be found at:

https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#pipe-dockerfile-through-stdin

## Transcript

Everyone is Ell Marquez with linuxacademy.com. And today we're gonna talk about the Docker file. 

Now, if you're following along with our quick start guide, you know that we just talked about Docker Images and honestly, it's a lot of beating around the bush trying to figure out how to teach images without delving into the Docker file what better video to follow up than for us to go ahead and write our own Docker file we're gonna do is we're gonna try to tackle our example that we had here with our lucid chart, we're gonna build an image that uses ubuntu as its base. 

Then we'll go ahead and do an update and will install Python three. 

| | Onboarding | |
| -- | -- | -- |
| | apt-get install python3 | |
| | apt-get update | |
| | Base image: Ubuntu 16.04 | |

vanheemstrasystems/onboarding

And we're not gonna go too far into all of the different configuration changes that you could do with the Docker file. If you'd like to tackle that, go ahead and follow up to this course with the Docker deep dive course. 

But in the meantime, let's go ahead and get behind that command line and start getting our hands dirty. 

So we're logged into the same environment in which we did our scripted Linux install. 

```
$  docker images
```

If you recall, we didn't pull down any images. So if we do our docker images command, we will see that we have no images on our system. 

```
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
ubuntu        16.04     9499db781771   5 weeks ago     131MB
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```
***Note***: we did have some images, but not to worry : )

What we're gonna do is we're gonna create our own image using this as our template. 

Now, you can think of this all in boarding square here, just the directory that we're working in this we'll go ahead and create that directory. You know what? Let's not capitalize that because it's just not good in Linux to have some random capital letters. 

```
$ cd ~
$ mkdir onboarding
```

I'll go ahead and CD into that directory and I'll create my Docker file. 

```
$ cd onboarding
$ vim dockerfile
```

Now, you don't actually have to use the term Docker file because you can specify what follow your gonna use. However, by default, it looks for that Docker file. So the first line is gonna be that from command. Where are or what are we? What are we basing this image on? 

```
FROM ubuntu:16.04
```
dockerfile

When we saw our ubuntu image in the previous video, we saw that it's set from scratch because they were creating it completely from scratch and pulling in that tar file. However, we're gonna base ours on that ubuntu 16.04 image. 

Next we want to update it. So the command that we're going to run is going to be at get update. 

```
RUN apt-get update
```
dockerfile

Next, we're gonna want to run the command at get install Python three, with no prompting (hence -y). 

I do, however, know that you only really have to do apt install. I'm sorry. Old habits die hard. Let me go ahead and add that dash y flag in so that we're not prompted to accept it. 

When you're automating something you really don't want any prompts inside of exit can definitely break your script. I forgot the word installer. 

```
RUN apt-get install -y python3
```
dockerfile

Technically, this is everything that we need.

This is exactly what we need to be able to get our on boarding image up and running. There are two things I'd like to know here, once you see that I capitalize are from in run statement. Although that isn't mandatory and the Docker file can run without this capitalization. It's what we call best practices. Next is once upon a time when Docker first started, there was an instruction called maintainer that was best practices to use, so you'd see an image looking something like this. 

```
MAINTAINER ell.marquez@linuxacademy.com
```
dockerfile

So maintainer has since been deprecated and it was really a set of instructions, kind of looking, awesome field that led individuals know who was maintaining. You know, if they had an issue, who should they contact? It's still in use, but the way that it's used now it's still somewhat in used. But really, it's used now as a label. So if you did want to have that maintainer status, you would simply go ahead and use label as your instruction. 

```
LABEL maintainer="ell.marquez@linuxacademy.com"
```
dockerfile

So that's all we need. 

We should be able to exit out of this video. 

Let me give it one once over just to make sure I didn't make a silly typo. Well, go ahead and write and quit. 

```
wq!
```

Then we can use the command docker build. 

```
$ docker build dockerfile
```

Be building the image and I could give it the name of the file on many years or more commonly, you'll see a dot that means build using the docker filed that is in this current directory. 

```
$ docker build .
```

So we see our build context, which is what we wrote in that file being sent to the Docker daemon. 

The first step is to go ahead and pull down that image from the Docker repositories because we didn't have it in our library. The scroll up here and we can take a little bit of a closer look. So we saw Step one of four was from Ubuntu 16.04 that's what we told it. It pulled it down from the library, and you see those four layers that we've discussed previously. 

```
Sending build context to Docker daemon  2.048kB
Step 1/3 : FROM ubuntu:16.04
 ---> 9499db781771
```

Once it's been pulled down, it does step to it, adds the label maintainer, and you can see my email address there. Now I want you to note something. It says that this is running in and it gives an I D. As it's pooling instructions. It's actually creating a container for that toe a current. So he had a pool and we had a boon to 16 04 happened here. It then gave us and I d number. I want you to go ahead and note this this a 51 because it's gonna come across in just a bit. Then we had our step to our label that ran in this container and as soon as the instruction adding that label was done, it going ahead and terminated that container, Then we have another container, then we have another I D. Here This is called an intermediate image. It's an image layer that is created and kept in cache but it's only kept long enough for this build process to occur. It is not an image that you would have access to, so Step three is to do that RUN apt-get—RUN apt-get update and that goes ahead and occurs inside of another container. We see the update occurring here, and as soon as the update is done, it removes the container and we get another one of those intermediate image layers. 

```
Step 2/3 : RUN apt-get update
 ---> Running in 387075685e23
```

Step four goes through the install process of Python three, which is run in its own container, and we work our way down once the container. Once the instructions have completed, that container goes ahead and is removed and we get our new image. 

```
Step 3/3 : RUN apt-get install -y python3
 ---> Running in 12a9d4a430f4
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
```

I d now have you noticed the intermediate image layer is the same as our final build number? That's because this is it. You're done. This is not an intermediate layer. It is your actual image. 

```
Removing intermediate container 12a9d4a430f4
 ---> f70b04ba7ac3
Successfully built f70b04ba7ac3
```

We can prove that by doing your Docker images. And here you see your image. I d is the same as what was built. 

```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
<none>        <none>    f70b04ba7ac3   11 minutes ago   198MB
ubuntu        16.04     9499db781771   5 weeks ago      131MB
hello-world   latest    bf756fb1ae65   12 months ago    13.3kB
```

Let's go over it one last time with our lucid chart, as it might make it clear. So we had right here. We sent the context to the Docker Damon. That's what was inside of our file. And step one was from Ubuntu 16.04 to have that image pulled. That would be this right here. Then I decided to add something a little bit different here. And that's because we went ahead and did our label maintainer from there. We went ahead and did our run at get update. That's gonna be here. And so there was a container container 962b was created with this base image and an update was run. When that update was completed, the container was closed. So it removed that container. Then a container was spun up. With that Intermedia image being the Ubuntu 16.04 that had been updated. There was an intermediate image, which was this right here. A container with this image layer was spun up and python three was installed. Once that was completed, that container was removed and what was left, which would be in this image layer here was our actual layer that would keep. Although we had an image layer built here and here with our maintainer label, those were simply kept in cash. And as they weren't what we requested, they were not kept on the system. But if this is the case, then what's this image here? Well, it's our Ubuntu image which we pulled down from the Docker Hub in order for us to be able to create our new image because it's what our new image was based on. 

Okay, guys, that's it. 

That is how you start out by building your own Docker Images. Hopefully, right now, you're feeling a little comfortable with the concept. And you went I'd encourage you to stick around active this video if you follow it along with your own environment and build out a couple of different Docker files, see what changes you can make and how that changes the resulting image layers and you know it. Just have fun and get to know your Docker environment. 

For now, though, you can go ahead and close out this video and continue on with your Docker journey. 
