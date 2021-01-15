# 1500 Docker Hub Basics

In this video, we will discuss what the Docker Hub is and go over the differences between repositories and registries. We will walk through how to create our own Docker Hub account and create our first Docker Hub registry. By the end of this video, you should feel comfortable navigating through the Docker Hub GUI.

Additional information about official registries:

https://docs.docker.com/docker-hub/official_repos/#how-do-i-create-a-new-official-repository

## Transcript

Hey, everyone, it's Ell Marquez with linuxacademy.com and today we're here to talk about the Docker hub. So if you've been following along with our Docker Quick start Series, you have docker up and running. And in fact, we did cheat a little bit and we went ahead and ran our first container. But how did that happen? Well, the way that it happened was that we pulled down an image, but I didn't really address where this image was coming from. 

The image that we pulled using our standard insult of docker came in from the Docker Hub. Now, if you are unfamiliar with the Docker Hub but you do have perhaps a little bit of a tech background you may be in familiar with GitHub. Now we use GitHub in order to go ahead and store code that we want to share perhaps within our company, perhaps within the world. GitHub allows us to do this—I'm sorry—Docker Hub enables us to do the same thing with our docker images. Although Docker does enable us to be able to have publicly hosted images as well as privately hosted images. But we'll get to that in just a bit. 

When we delve into actually seeing Docker Hub in action and behind me, you're going to see two resources one is going to be the Docker Hub Main Web page, and the other is going to be our lucid chart that I'm gonna be using to hopefully be able to show you what's going on. So what you see on our lucid chart is first of all we have Docker and Docker is the docker engine, which we just installed on our server. It's what enables us to be able to run these containers within our server environment. Then we add to that the hub, and if you know the term hub, it means kind of the heart or the core of something. So we like to think of the docker. Hub is kind of the heart in the core of what helps docker run. We pull that together and we have the docker hub. The docker hub is referred to as a registry, and within this registry, we have repositories very similar to when you are pulling something in from, let's say, red hat and you're pulling in from those red hat repositories. Well, when you're pulling down an image, you'll be pulling down an image from a docker repositories that's held on the Docker Hub. Now, I did stay earlier that this is the standard installed because Docker really can work with any hub that's available out there. We have private cloud or public cloud companies that do offer their own hubs. And Docker does enable you to be able to host your own private repository or private a registry within your company so that it's not accessible to the outside world. This is great for companies that really do use Docker for proprietary information. That's a lot to handle. So let's go ahead and take a few step backs and let's just about the Docker hub on its own. 

So in order to use the docker hub, you're going to want to have your own account. So let's go ahead and turn our attention to the screen and get that set up so that we can get to learning. So the first thing that I'm gonna do is I'm gonna go ahead and close out or lose the charts so that if you're on a mobile device. You're not struggling to see what it is that we're doing on the screen. 

https://hub.docker.com/signup

Now the first thing that you are gonna want to do is pick your docker ID. Now, please keep in mind that you are more than likely going to be sharing this ID with others, so please remember to keep it to something that you're gonna feel comfortable sharing. So if you follow me on Twitter, you'll know that my secret alias is ellopunk, and I'm going to go ahead and choose that for my ID. 

```
Docker ID: wvanheemstra
```

Then you'll want to go ahead and enter your email address and choose a secret password. 

```
Email Address: wvanheemstra@icloud.com
Password: *****
```

Then you'll want to go ahead and take the time and read the team terms of service as well as your privacy policy and your data processing terms. Now, I know that your first instinct is going to be to skip these, but go ahead and read them because if you're gonna be an active part of the docker community, this is really going to layout the foundation to how you're gonna be interacting with the docker hub. Also remember that You know, our first instinct is to opt out of getting any emails. However, I have found these emails to actually be valuable when I'm wanting to stay up to date with what's going on with Docker. So I'm gonna go ahead and agree to all of these, and then we're going to play the captcha game. 

Now, I'm gonna go ahead and just kind of edit this section out, fast forward through it so that you're not having to watch it. Now that you know that I am officially not a robot, we can go ahead and sign up. 

All right, we're almost ready to go. 

So let me jump back over to my email and get this confirmed and we'll be ready to start using the Docker Hub. And now I've kind of clipped out some personal information from this shot. But in order to confirm all you'll need to do is go ahead and click that confirm your email as well as ensuring that you do this within two days. So let's go ahead and confirm that email. 

All right. It's a simple is that we're logged in. Now we have the option of being able to create our repositories, we can create organizations or we can even explore other repositories. This is where I'd like to get started, because it's really at the core of how you'll be interacting with the docker hub. 

```
https://hub.docker.com/orgs/vanheemstrasystems
```

So as the screen is loaded, you'll see that we have a few different repositories showing up used the nginx, alpine, busybox and underneath you're going to see the tag of Official. So the docker official repositories are a set of Docker Repositories that are hosted on the docker hub that are designed to offer a few specific use cases. 

```
https://hub.docker.com/search?q=&type=image
```

For example, you have your base OS repositories. That's gonna be your ubuntu your CentOS and these are there to serve as a starting point for a majority of users. They're gonna provide a drop in solution for popular programming languages, run times, data stores and other services, very similar to what a platform as a service (PaaS) would offer. You're going to have their going to also exemplify the docker file best practices, and I'll show you that in just a second, as well as provide a clear documentation to serve as a reference point for other docker file authors. 

Maybe that's gonna be you some day, so these will give you great examples of what your Docker files should look like. They're also gonna ensure that security updates have been applied in a timely manner. And this is really important when it comes to being part of an official repositories as they become some of the most popular ones available here on the Docker Hub. So let's go ahead and click on this nginx repository as its right at the top and kind of given example of what this looks like. 

```
https://hub.docker.com/_/nginx
```

So this is the official repository for nginx. You can see that at the top of your screen as well, to the side of that giving you what command you're going to need in order to pull this image. So on your command line, you simply type docker pull nginx. I'm actually gonna be using a different repository in order to show you what I think is an amazing example of a way to up keep repository. And that's gonna be our hello world image. So let's go ahead and go back and search for that hello world image. 

```
https://hub.docker.com/search?q=hello-world&type=image
```

Here we can see the official version of hello world and we could also see there are other versions that have been made available to the public, where others have kind of put their own spin on things. We go into our hello world repository. 

```
https://hub.docker.com/_/hello-world
```

We can see the simple command that we ran Docker pull Hello World. 

```
docker pull hello-world
```

We can see the get hub in which to file issues. 

```
Where to file issues: https://github.com/docker-library/hello-world/issues
```

We can see where we can get help. 

```
Where to get help: the Docker Community Forums, the Docker Community Slack, or Stack Overflow
```

If we're having issues with this image, they'll even show you an example of the output that you'll see if you do a docker run Hello World. 

```
Example output
$ docker run hello-world

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


$ docker images hello-world
REPOSITORY   TAG     IMAGE ID      SIZE
hello-world  latest  bf756fb1ae65  13336
```

It looks very similar to what the output should have been when you ran that container through your install process. This is a great example of providing information for a specific image because they even give you information on how this image was created, as well as licensing information for it. Now I will say that this is not available through every image because it's really the image maintainer the creator that is providing what information they're gonna share to the outside world. This is one of my favorite images, however because of the depth of information that is really put on their docker hub page. 

Now I do know that this video is getting a little bit longer than any of the other videos in this course. However, I think it's because this is how important the docker hub is to your success with using Docker. Even if you're using your own private repository, much of the information is going to be the same and in the way that you interact with it. 

So let's go ahead and scroll back up and work on creating our own repositories so we'll go over to ***create***. We'll have the option to create repositories, to create an organization, let's say that we were working with other developers or even create an automated build that's gonna be more of a deep dive topic. 

Let's go ahead and just go into creating our own repositories. So I'm gonna use this as a docker quick start, then we'll enter a short description. Now, you see here that you have a few options for visibility. You have that as a public repository, which means that the whole world will be able to use them. That's what I'm gonna choose for us so that you're able to interact with this repositories later on, as you're taking this course, and we also have the option to set it private. This is something that I might do if let's say that I was working with another course author on developing a specific image to use, however It wasn't really ready for the rest of the world yet. So let's go ahead and choose public. Hold on. We have an error. It says that we need to enter a valid repositories name, which means that we can have no spaces, no social characters. So let's go ahead and get rid of that space. There you go, let's give it a try. 

```
https://hub.docker.com/repository/docker/vanheemstrasystems/dockerquickstart
```

As simple as that, we are up and running with our own repository here. 

So what if I wanted to create an additional public repository? Let's say that we were gonna go ahead and start working on that docker deep dive course. Well, it really wouldn't be a problem. That's because docker allows you to have as many public repositories, as you need to. You can share all your images with the world. However, if you wanted to have more private repositories than just the original one. This is where you're going to start needing to look at different pricing plans available through docker. Let me go ahead and take show you that before we move on. 

```
https://www.docker.com/pricing
```

So this is the billing and pricing information, and you can see at this time with our free plan, we're allowed one private repository as well as one parallel build. This is a way to have our builds occur quicker by allowing for them to occur in a parallel manner. I guess that's gonna self explanatory there. But we're not gonna go into that right now. We're focused on our repositories. You also can see that if let's say you get a micro plan, you can have up to five and up to your extra extra large, which you can have 500 private repositories. Feel free and play with this on your own. 

But for now, I think we can kind of get back on camera here and wrap this video up. If you'd like to learn a little bit more and encourage you to take our docker certified associate course, which dives deeper into these subjects. But for now, that's all we have when it comes to the docker hub. So go ahead and close out this video and continue on with your journey
