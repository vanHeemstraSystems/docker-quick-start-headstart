# 1600 Docker Images

In this video, we will discuss what Docker images are and how we can use them. This video ties into the next lesson, in which we will tackle creating a Docker image.

## Transcript

Hi, everyone. It's El Martes from Linuxacademy.com and today we're gonna be discussing docker images. 

Now, one thing that I want to ensure that you're aware of is it's really difficult to discuss Docker just one concept without pulling other concepts into it. For example, when we did our docker install, we went ahead and pulled down a docker image and ran a container from it to ensure that our environment was working. The same thing is gonna occur when we discuss docker images because we'll need to discuss a little bit of the docker file and running containers. Please understand that we'll go further into those subjects and subsequent videos. And we're really gonna just be focused on understanding how we create docker images and also what a docker base image is. 

So I built out a story for you because this is really how I learned. 

Let's pretend that I work for a development company and I'm in charge of on boarding let's say junior developers just example, but I want my developers to be happy, so I'm not gonna tell them what type of computer to use. You want to develop on Windows, Mac OS, Linux, Whatever floats your boat, you're good. But what I want to ensure is that you're all writing the best code for us to write, to push into production and in production, we happen to use a ubuntu 16 04 And so what I'm gonna do is I'm gonna pull in the base image from the Docker Hub,  the ubuntu repository, which is going to be our base image of ubuntu 16 04 

```
Base image: Ubuntu 16.04
```

Now, I want to make sure that everybody is up to date and running the most secure containers that they can and most secure OS that they can. So I go ahead and I do that app get update. 

```
apt-get update
```

Now all of our developers will be coding and python3. So I go ahead and install Python3 as well. 

```
apt-get install python3
```

What I can do here, then, is I can take this image which I've created, and just to let the elephant out of the bag. We do so by using a docker file that will be discussing it a bit or we discussing in a different video. So I take this image which I have then created and I can push it back up into that repository which we created called ellopunk. Then when it's sitting there, when our new developer comes in and says, All right, Hey, I've been hired. How do I get started? Instead of just giving them a sheet of all the things they have to do to get their computers set up the way that we wanted to, I could see you know what? Just go ahead and pull down my get started image from ellopunk. That's it from our ellopunk repository. 

Then, just to make sure that your environment works exactly the way that we wanted to, why don't you write a small hello world application and then go ahead and push that up to the Linux Academy, get hub so that we can all see that you're up and running? 

All they would need to do is go in and pull that getting started image. They would go ahead and copy over the files for their hello World Python script. Then they could push with essentially become a new image back up into the docker hub. 

No, that's as clear as mud. Don't worry. 

We're gonna be spending next few minutes together, actually going through and seeing what this looks like on the command line. 

So I'm gonna go ahead and get off screen so you guys can focus on that and we'll see you on the other side. 

So the environment that were logged into is the same environment that we did our scripted Linux docker install. So in order to see if we have any images there, we can use the command docker images. 

```
$ docker images
```

```
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   12 months ago   13.3kB
```

You see that we currently have no images available (except from previous download). 

So we could pull one down using the command, docker pull And let's say that we wanted to pull that ubuntu image so we could do docker pull And let's say that we were just a type enter here Well, that it would pull down Whatever image is tagged by ubuntu as their latest image. Sometimes the latest image might not be the most newly available. For example, if they have an edge release that, perhaps is their latest, however, they're stable release is tagged with something perhaps unstable. If we wanted to pull down ubuntu 16 04 then we would be ubuntu 16, 04 So, docker pull , from our ubuntu repository the image 16 04 

```
$ docker pull ubuntu:16.04
```

Now, I want you to notice that this isn't just one pull. You actually saw multiple pulls occurring as well as multiple pulls having been completed. You can see that we had one pull here 234 

```
16.04: Pulling from library/ubuntu
be8ec4e48d7f: Pull complete 
33b8b485aff0: Pull complete 
d887158cc58c: Pull complete 
05895bb28c18: Pull complete 
Digest: sha256:3355b6e4ba1b12071ba5fe9742042a2f10b257c908fbdfac81912a16eb463879
Status: Downloaded newer image for ubuntu:16.04
docker.io/library/ubuntu:16.04
```

What you're seeing here are ***Docker image layers***. 

Images on docker could be composed of several layers. 

So, for example, in this image, once it's completed, we would have our base image which would now be ubuntu 16 04 that would be one layer. 

Our update, which has created a different change on that image, would become another layer and then Python3 would be yet another layer. 

In order to really understand what caused these layers to be created, it's best to really look at the docker file now. 

I'm not gonna be spending too much time on the ***Docker Files*** will have its own video. 

However, I did want you to be able to see what was occurring. 

*** WE ARE HERE ***

I could check out our official ubuntu image. I go down to 16 04 and I can see the docker file that it was used in order to create that ubuntu 16 04 image, every change that occurs to this image is going to cause a new layer. So they're saying from scratch, meaning that this isn't based on anything else. We're going to add this file. Then we're going to run this section. There's might be thinking, Well, why didn't that Cause multiple layers? That's because they scripted it in such a way that this is really only running one command. You can see that by your  and and commands here. So that was later two. Then layer three is gonna be the removal of this, then layer four, is going to be your maker change. So now that we have a little bit more transparency to what it is that we've pulled from the Docker Hub, let's take a look at how we are going to be interacting with our docker image. So let's go ahead and do Docker Images again so that we can see the image on our system. There's a bit of information here. Now I'm gonna go ahead and just close out my LucidChart for a little bit so that you guys are better able to see the information on the screen. Okay, so running Docker image we see the repository that this image was pulled from was are ubuntu repository. Now this image was tagged with the version being 16 04 Now One thing I want you to understand is that a tag really has absolutely no value when it comes to the image other than what we put on it. Think about tags as one of those labels that comes out of the label maker. You can write whatever you want on it, and it just represents whatever value you put on it. So we could use tags to label version numbers. We could use them to label the person who's created it. You have a tag called maintainer that is a docker standard for that. You know the tag is going to be L's image, or we can use tag to, we can use tags for separating development from production. Then we have our image ID Now this ID is used to uniquely identify this image. It's almost like the images name, though we can refer to it as ubuntu we can also  refer to it by its image name to be able to interact with it. So whereas I could run a container with Docker Run ubuntu 16 04.  I could also run the exact same container with a command docker run and the image ID Now something interesting to note is that this image ID, isn't actually, it's full image ID We can add the no trunk flag in order to be able to see the full ID. You can see that it says that it's a Sha256 image ID. What it really is is a hash, a sha256 hash of all the image layers that were created to compose this to compose this image. Later on, we can discuss about how this could be used in security to ensure that you are pulling the image that you believe that you are pulling all right. I wanted a hop back on the screen just to say that I hope that you now have a better understanding of what a docker image is of how a docker image is composed of layers and how we're able to change what essentially is our base image into a whole new image that fits our needs. For now, though, you can go ahead and close out this video and continue on with your journey.
