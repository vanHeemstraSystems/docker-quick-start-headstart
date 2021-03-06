# 2100 Redirection: Docker Container Ports

In this video, we will learn about Docker ports. While we will discuss Docker specifically, the concepts we'll learn in this lesson apply to every container technology. By exposing ports, we can create internal connections to locally hosted applications and then, when we're ready, publish those ports to make the connection available to the outside world.

Note: if any rpms need to be installed, use 'yum install $rpm_name' to install it.

To install elinks:

CentOS 7: ```sudo yum -y install elinks.x86_64```

CentOS 8: ```sudo yum --enablerepo=PowerTools install -y elinks```

Ubuntu: ```sudo apt install -y elinks```

## Transcript

Hey, everyone, it's El Marquez back with your Docker Quick Start series. Today we're gonna be discussing Docker ports or maybe more realistically, container ports, because the technology behind it and the concepts really kind of open up to any containerization product that you're using. 

So what we're covering today is the ability to have access to your container, perhaps from just the internal host, just the server or laptop that you're on, or when you're ready to publish those ports to the entire world. Now a quick note before I disappear and we get to the meat of the subject. If you watch the previous quick start version of this course, note that ports and volumes were included in one video in one lesson. I've decided that it's best to split those up because I have a lot to say on both subjects. With that out of the way, go ahead and get your command line ready and follow along. 

So here we are logged into our system, and the first thing that we need to do is see what's available on our system already so that we don't get confused in the process of creating new containers. So let's do our Docker Container LS, Docker Container LS -A and Docker Images or Docker Image LS. 

```
$ docker rmi f7
Untagged: wvanheemstra/onboarding:v1
Untagged: wvanheemstra/onboarding@sha256:dbcb7ee1ff2630b5e058be288de63d219d4472125ac7926e99806b42a2ef7cec
Deleted: sha256:f70b04ba7ac39dc63182641c4ae20d90cfa8804800a95f7ca6d7fd2506af937d
Deleted: sha256:989bb4a759702308ae7a070b33b9f9947eb9bb48ab772d97943a6eaf9afdd04c
Deleted: sha256:458e24e94b880afa71438d0cedf6d0d9dd6c893d805d508428eacf8878e51fe4
Deleted: sha256:f40485a002f52daa539c4ebf3a9805d74a0396eacb48d09f3774b2c9865a43db
Deleted: sha256:4c823febe808dcc9c69e7b99a91796fcf125fdde4aac206c9eac13fcfd4ffba3
Deleted: sha256:ea2e76a9d2f2be4a60d0872a63775f03f9510d7a0aa6bdc68a936e9a7b7b995a
Deleted: sha256:da2785b7bb163ff867008430c06b6c02d3ffc16fcee57ef38822861af85989ea
```

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```
$ docker container ls -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```
$ docker images
REPOSITORY                TAG       IMAGE ID       CREATED        SIZE
```

```
$ docker image -ls
REPOSITORY                TAG       IMAGE ID       CREATED        SIZE
```

Now, you see, there really isn't anything going on in this system right now, so we really shouldn't have any conflicts when we're talking about port accessibility. 

So let's go ahead and clear our screen and we'll start off with our usual Docker Container run command. 

Now, this time I'm going to use a - D flag so that this container runs detached and we're gonna go ahead and use a brand new image and that's our Nginx in it. 

```
$ clear
$ docker container run -d nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
6ec7b7d162b2: Pull complete 
cb420a90068e: Pull complete 
2766c0bf2b07: Pull complete 
e05167b6a99d: Pull complete 
70ac9d795e79: Pull complete 
Digest: sha256:4cf620a5c81390ee209398ecc18e5fb9dd0f5155cd82adcbae532fec94006fb9
Status: Downloaded newer image for nginx:latest
5340f7259a1fe35c7aae0e6d436eb2472ab1fb5c012f0c63bf77b39947fc18eb
```

This has a little bit more of a real world practicality than our hello world image or even the new on boarding image, which we've developed. Once this is done, we can do a Docker Container LS, and we can see that we now have a new container up running, starting with the container ID of 53. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS     NAMES
5340f7259a1f   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    objective_blackburn
```

Now actually, since there are no other containers on this system, we could just refer to it as container five. Another thing that you'll notice is that under our ports we have port 80 available on this system. It's port 80 TCP, and it's available or exposed in the container. 

Now, the reason that I pause and kind of overemphasize the word exposed is there are two terms that you'll want to be familiar with. 
One is exposed and the other is published. 

***Exposed*** opens up and exposes of the port inside of the container and makes it available to local host and Internal Services so I'll be able to actually go into this container as usual but also be able to use services is like elinks to connect to the container on Port 80. We'll actually do that in just a bit.

To ***publish*** a port, both the host port and the container port can be specified, and they're basically linked to one another so that we have accessibility to the container from the outside world. 

Don't worry, we'll use examples of all of this so you can better understand it. But we need to understand right now is with this port, port 80, being exposed in the container we could connect to it with service is such as elinks. However, we could not connect to it from our Web browser or using the public IP of the server. Now, how do you know what ports are going to be exposed whenever you create an image? Well, you can use the command  Docker image history and then tell them what image you'd like to look at, so that would be Nginx, and we can see that Port 80 is exposed on this container.

```
$ docker image history nginx
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
ae2feff98a0c   3 weeks ago   /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  STOPSIGNAL SIGQUIT           0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  EXPOSE 80                    0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  ENTRYPOINT ["/docker-entr…   0B        
<missing>      3 weeks ago   /bin/sh -c #(nop) COPY file:0fd5fca330dcd6a7…   1.04kB    
<missing>      3 weeks ago   /bin/sh -c #(nop) COPY file:0b866ff3fc1ef5b0…   1.96kB    
<missing>      3 weeks ago   /bin/sh -c #(nop) COPY file:e7e183879c35719c…   1.2kB     
<missing>      3 weeks ago   /bin/sh -c set -x     && addgroup --system -…   63.7MB    
<missing>      3 weeks ago   /bin/sh -c #(nop)  ENV PKG_RELEASE=1~buster     0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  ENV NJS_VERSION=0.5.0        0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  ENV NGINX_VERSION=1.19.6     0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  LABEL maintainer=NGINX Do…   0B        
<missing>      3 weeks ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B        
<missing>      3 weeks ago   /bin/sh -c #(nop) ADD file:3a7bff4e139bcacc5…   69.2MB  
```

So let's go ahead and clear our screen and see what this would look like. 

```
$ clear
```

So let's do our Docker Container LS so we always remember what continued we're working with. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
5340f7259a1f   nginx     "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   80/tcp    objective_blackburn
```

I know we only have one now, but it's best to get into the spirit of being able to see all of the containers in your system before we start running commands. 

Then we'll do a Docker Container Inspect and I'm gonna grab out the IP address for this container. 

```
$ docker container inspect | grep IPAdd
"docker container inspect" requires at least 1 argument.
See 'docker container inspect --help'.

Usage:  docker container inspect [OPTIONS] CONTAINER [CONTAINER...]

Display detailed information on one or more containers
```

Now, as I said, it would be really helpful if we specify what container we're working with so let's try that again and use our ID of 53. 

```
$ docker container inspect 53 | grep IPAdd
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",
```

Now you see, this container is running on 172.17.0.2 so let's go ahead and do elinks to it. 

```
$ elinks 172.17.0.2:80
```

Now we could specify port 80 but as web servers by default run on 80 elinks does not require that. 

```
$ elinks 172.17.0.2
-bash: elinks: command not found
```

Install elinks if it is not yet installed, see https://tekneed.com/how-to-install-elinks-rhel-8-and-lynx-in-rhel-8/

```
$ cat /etc/centos-release
CentOS Linux release 7.8.2003 (Core)
$ sudo yum install elinks -y
...
Complete!
```

```
$ elinks 172.17.0.2
Welcome to Elinks!

Press ESC for menu. Documentation is available in Help menu.
                    [OK]
```

Confirm with OK

```
Welcome to nginx!

If you see this page, the nginx web server is successfully installed and running. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.
```

We can see Nginx is, in fact, up and running. 

Now if I tried to do the same command, however, and worked with a local host instead, now you can see here that we're unable to establish a connection. 

Exit Nginx window by choosing "OS Shell" from top left menu, click over it if not visible.

```
$ elinks localhost

Unable to retrieve
file://home/cloud_user/localhost:

No such file or directory
        [OK]
```

That's because we don't have our local host listening on Port 80 running Nginx. 

So let's go ahead and try that command again. 

We'll do our Docker Container run -D but this time we'll use a capital P option with our Nginx image. 

```
$ docker container run -d -P nginx
48812a5ebfefc01c7aafb07632db32d7deab8f62718ba88e2a3bf0d20c29a642
```

Docker Container LS will let us know which container is running. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS          PORTS                   NAMES
48812a5ebfef   nginx     "/docker-entrypoint.…"   About a minute ago   Up 43 seconds   0.0.0.0:49153->80/tcp   sweet_galileo
278dd40f4569   nginx     "/docker-entrypoint.…"   41 minutes ago       Up 40 minutes   80/tcp                  nervous_kilby
```

Now that we have it going, we can see what occurred. So we have on port 49153 of our hosts system being mapped to port 80 of the container. 

Now if you've been using Linux Academy servers for a while you know that that port really doesn't do us any good because we don't have access to it, by the way that our servers are made. So what happens if we only have specific ports that we can use and we want to specify port? Let's try Docker Container run -D but this time, let's do a lowercase P. Now we can say that we want port 80 of our host to be made to port 80 of our container, and I'll go ahead and use image HTTPD (i.e. Apache Web Server) just to prove to you all that this is not another container that we've already created, that we're a able to connect to. 

```
$ docker container run -d -p 80:80 httpd
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
6ec7b7d162b2: Already exists 
17e233bac21e: Pull complete 
130aad5bf43a: Pull complete 
81d0a34533d4: Pull complete 
da240d12a8a4: Pull complete 
Digest: sha256:a3a2886ec250194804974932eaf4a4ba2b77c4e7d551ddb63b01068bf70f4120
Status: Downloaded newer image for httpd:latest
4559deaefcb4aeb4363f3d21245066df0b97900b240c44c6c6cba3e67b7e7244
```

But before I clear my page, I realized that I did miss a little bit of information here. 

Where did this port 49153 come from if we never specified it? 

Well, this is the ephemeral port range, and it's typically import between 32768 and 61000 that its chosen from really just kind of depends what the  IP local port range is set to as the kernel perimeter within your box. 

But that's really more of a topic for a deep dive, and so let's go ahead and clear our screen and see if we can connect to this Apache container. 

```
$ clear
```

Now we could make use of a great tool by a good friend of mine, Major Hayden. And we can do a curl -4 so we can get an IP address to icanhazip.com. This gives us the IP of our box. 

```
$ curl -4 icanhazip.com
34.244.117.247
```

Now, remember, if you're following along, you'll need to get the IP for yours, and we can use an elinks to that public IP. 

And we could specify port 80 but as that's the default port for an Apache page we can just go ahead and type enter. 

```
$ elinks 34.244.117.247
```

What do you know? It works. We get the default Apache page. 

```
It works!
```

Exit Apache page by choosing left top menu [ File ] [ Exit ].

Let's take one last look at our container LS to see what it is that we covered in this video. 

```
$ docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                   NAMES
4559deaefcb4   httpd     "httpd-foreground"       11 minutes ago   Up 10 minutes   0.0.0.0:80->80/tcp      sweet_williams
48812a5ebfef   nginx     "/docker-entrypoint.…"   17 minutes ago   Up 16 minutes   0.0.0.0:49153->80/tcp   sweet_galileo
278dd40f4569   nginx     "/docker-entrypoint.…"   57 minutes ago   Up 57 minutes   80/tcp                  nervous_kilby
```

So we know that by the use of a lowercase p, we can specify what port we want to match to what port in our container. 

```
0.0.0.0:80->80/tcp
```

And we know that with our next container, we can use a capital P to have a random port chosen that will be mapped to a local port on our container. 

```
0.0.0.0:49153->80/tcp
```

And finally, if we do absolutely no flags. We just spin up a container we'll only have the port that was exposed in the Docker file for that image. 

```
80/tcp
```

Now there's a lot more that could be done with Docker ports than what we've covered here today. That's one of the downfalls of a quick start is that we really can't do a deep dive. So if you want to learn more about Docker ports, I'd really recommend that you go take our Docker deep dive course. 

For now, though, you can go ahead and close out this quick start video and continue on to learn about Docker Volumes.
