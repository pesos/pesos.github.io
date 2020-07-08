---
 title: "Delving into Docker"
 tags: docker containers
 author: Bhargav SNV Aditi Ahuja
 show_author_profile: true
 ---

Introduction
============

What is Docker?
---------------

Docker is a set of tools that allow us to easily run containers and containerised apps. Why use Docker and these so called "containers"?

Well, containers are extremely useful as they are very lightweight and have minimal overheads. We can package an app along with just its dependencies and can isolate this into a container. These containers can then be run on absolutely any platform with a Docker engine. It has other benefits too like minimal storage requirements, resource isolation, security, namespacing (isolating resources per process or a group of processes), availability and elasticity in the cloud, and much more!

These containers which we can package and ship are called *docker images*. Put more accurately, an image is essentially a file system snapshot along with a start-up command.

From [docker.com](docker.com),  
> "Docker container image is a lightweight, stand-alone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings."

![docker-image](https://user-images.githubusercontent.com/48997495/86560018-05f44a80-bf7b-11ea-97e7-ba85b7982d4c.png)

Here the file system snapshot is essentially a copy of a normal file system at a given point of time. It would have a bunch of packages installed, some configurations, and some dependencies too. All of this is stored here (but nothing unnecessary!). The start-up command on the other hand is the command the container runs when brought to life. This could be the starting of an NGINX server, or an application that was built, or starting a service, it could be any valid command.

What are containers?
--------------------

Okay so that's Docker, but what on earth is a container?

A container, put simply, is a small portion of your computer running all by itself. Let's put that in a better way. A computer would have it's own CPU, Hard Disk Storage, RAM, Network card, etc.

![computer-resources](https://user-images.githubusercontent.com/48997495/86560052-173d5700-bf7b-11ea-8177-95acafd55a6a.png)

So a container allocates a portion of each of these resources to itself. It'll have it's own storage, RAM, CPU, Network, etc. Now that it has a small portion of everything, it can run by itself! Hence, an application along with the required dependencies are put into a container's file system and this can be run from anywhere!

![container](https://user-images.githubusercontent.com/48997495/86560043-1278a300-bf7b-11ea-8787-c3483a04dae3.png)

A little something to take note of here is that all these containers essentially run as Linux Machines. And Docker helps bringing them up, passing them around and all the other good stuff!

Wait... Isn't this just like a VM?
----------------------------------

Is an image the same as a virtual machine? Absolutely not! Docker containers running images are far lighter than a virtual machine given that they do not bundle an OS. A Virtual Machine on the other hand, does bundle an OS. Let's look at this diagrammatically.

![container-v-vm](https://user-images.githubusercontent.com/44526455/86824978-615b3100-c07e-11ea-8e70-6cc1def53ed5.png)

As we can see here, in the case of a docker container, only the required application along with it's dependencies are bundled up into an image. While in the case of a VM, we have the heavy overhead of an entire Operating System associated with every image!

Why use Docker and containers?
-------------------------------------

We've seen the benefits of using Docker and Docker containers, but how would these fit into the real world?

-	Portability: Since a Docker image can be run on any system which has a Docker engine, it makes it extremely easy to ship applications without worrying about dependencies and setup. This way a dev team can ship just a docker image to a testing team and the testing team can directly get started on it without going through the hassle of any setup!

-	Kubernetes: Kubernetes is a platform to run and manage containerised applications, often running many containers together in dynamic environments. It helps running cloud native apps and makes use of Docker internally. A containerised app is lightweight and easily deployed to the cloud. Since they are isolated, they can be easily scaled by just bringing up more containers (sort of)!

Hands on:Get familiar with the basics
==========================================

Let's get our hands dirty!

We will be working with NGINX, a web-server with load-balancing and reverse proxy capabilities among others, for this tutorial, using it as a web-server for now.

We'll start off with an image pulled from [DockerHub](hub.docker.com), an online repository of Docker images.  
'Pulling' an image is the Docker equivalent of a git clone i.e. downloading an image to work with it locally. So let's pull the NGINX image: Run `docker pull nginx`.

To list the existing Docker images, run `docker images` or `docker image ls`, analogous to the `ls` command. You should see `nginx` now listed in the output.

To run an NGINX container, use `docker run -p 80:80 nginx` and check it running on `localhost:80`. Let's customize our container a tiny bit now: * To access it on a different host port, use the `-p` flag for port mapping.  
 `docker run -p 90:80 nginx` let's you access the webserver on port 90.  
 * Docker assigns a name by default to all running containers. To assign a custom name, this case "test", to the container, use the `--name` flag: `docker run --name test nginx`. * The `-d` flag is used to run a container in the detached mode i.e. the prompt reappears after displaying the container ID.  
 * The `--rm` flag is used to automatically remove stopped containers.

To sum up, the complete command applying all of these flags goes as follows:  
 `docker run -d --rm -p 90:80 --name test nginx`.

-	Running `docker ps` or `docker container ls` lists the details of the currently running containers. Running this now will show you the details of `test`.  
-	Adding the `-a`(--all) flag, i.e. `docker ps -a`/`docker container ls -a` lists the stopped containers as well.

-	To stop the container, the syntax is `docker stop <container name>`, in this case `docker stop test`.

-	Starting and restarting a container can be done using `docker start <container name>` and `docker restart <container name` respectively.  
	That will be `docker start test` and `docker restart test` here.

	-	The container can be removed(deleted) once stopped using `docker rm test`, or if not stopped, using `docker rm -f test`. This is similar to the `rm` we might already be familiar with.  
	-	Deleting an image can be done using the syntax `docker rmi <image name>`. An image can be removed only if there are no containers using it.  

Diving deeper:
==============

docker exec
-----------

`docker exec` to put it simply, executes a command within a running container. The syntax is as follows: `docker exec -it <container ID/name> <command>`.

Let's see a few examples with the NGINX image:

-	Run `docker run -d --name test nginx`.

-	Running `docker exec -it test bash` opens a Bash shell within the container, used as usual.

-	Adding the `-e` flag allows setting the value of an environment variable.  
	Let's set a sample variable using the flag:  
	Run `docker exec -it -e num=10 test bash`.  
	An `echo $num` within the container will verify that it's been set.

-	Exit the shell and run the following: `docker exec -it test sh -c "ls"`.  
	This gives the contents of the container since it's equivalent to opening a shell and listing container contents,combined in one step.

-	The `-w` flag sets the working directory for the command to be executed.  
	Compare the results of `docker exec -it test sh -c "pwd"` and `docker exec -it -w /usr test sh -c "pwd"`.  
	The former returns the path `/`, whereas the latter returns `/usr`.

Dockerfile
==========

We just need to pull an image from DockerHub to get started immediately. But what do we do when we need to build our own custom image for say, an app we created?

This is where Dockerfiles and docker builds come into play. A Dockerfile is a plain text file with a set of commands and specifications which instructs docker on how to build an image for us.

Let's work with this using an example. Say we've built a simple static website and we now want to put that into a container and serve it with a Web Server. The easiest way to go about this, would be to copy our .js, .css and .html files onto an image hosting a web-server.

So this is what the Dockerfile would look like.

```
# Specify the base image
FROM nginx   

# Copy all website content into the container
COPY ./static-html-directory /usr/share/nginx/html
```

Let's go over these above steps one by one.

-	The first line `FROM nginx` specifies a base image. A base image is like a default image which we build on top of. In our case, we picked the NGINX image as it already has a web server setup and ready to host content for us. All we need to do is provide the content it has to serve.

-	The second step, `COPY static-html-directory /usr/share/nginx/html` copies all our files from our local system(i.e.host) into the container. The way this command works is `COPY /source/path /destination/path`. Where the `/source/path` is the path to the directory in our local system and the `/destination/path` is the directory inside the container where the files are to be copied.

To have some sample content to test it out, log into the container using `docker exec` and run `cat /usr/share/nginx/html/index.html` and copy the content. Modify it slightly, changing the message for example. Now add it to `static-html-directory/index.html` and copy it into the container.

And that's it! All that's left for us now is to run `docker build`. We'll get to that in the next section. But before we do here's a simple workflow for building custom images.

```
# Pick an appropriate base image to work with
# Syntax: FROM BaseImage
FROM ubuntu

# If needed, run shell commands here,  
# to maybe install additional components or configuration
# Syntax: RUN Command
RUN apt install python

# Copy necessary files, skip if none
COPY ./file.txt ./

# Specify a custom start-up command.  
# If this is omitted, the default start-up command of the image is used.
# The syntax for this command is where each argument of the command is put in double quotes and separated by commas.
# Syntax: CMD ["command", "with", "arguments"]
# Eg: if the command to run is "python -m SimpleHTTPServer 8000"
CMD ["python", "-m", "SimpleHTTPServer", "8000"]
```

Building custom Dockerfiles
============================

Now that we have a Dockerfile ready, the next thing to do is to build it. This is as simple as running the below command:

`docker build .`

This works only if the necessary files to copy and the Dockerfile are in the current directory. Let's take a deeper look into the docker build command.

The syntax is  
`docker build context [-f Dockerfile] [-t tags]`

This might be a little overwhelming at first, so let's go through it part by part. All the option placed with Square brackets [ ] are optional. We'll get to them soon. The only mandatory component is the `docker build context`.

-	`Context`, here specifies the directory in which the Dockerfile is placed. If in the current directory, we replace context with `.`, if elsewhere, we can provide the /path/to/that/directory.

-	The `[-f Dockerfile]`. By default docker looks for Dockerfiles named exactly as 'Dockerfile'. If we want to give it a file with a different name, we can specify it with `-f filename`.

-	The `[-t tags]`. This option is used to "tag" a name to the image being built. Although these are to actually control build version tags, we can use these to give names to our build locally. By doing this, we can later call the image directly by name rather than use an image ID generated at the end of build.

After understanding these options, we can build the image by running the below command. (Assuming our dockerfile is called Dockerfile and placed in the current directory).

`docker build -t simple-nginx .`

We have tagged it simple-nginx.

Running the custom image
========================

Docker run syntax: `docker run image [-p localPort:containerPort]`

-	The `[-p localPort:containerPort]`. This is used to setup port mapping between our local machine(i.e. host) and the container. By default, the container can make requests to the outside world, but the outside world cannot make requests to the container. As in our case, we need to allow HTTP traffic, we must make the HTTP port (80) on our container available to the outside world. We expose this port by mapping it to a port on our local machine.  
	So if we did, `-p 8000:80`, any request we make to port 8000 on our local machine would map to the container's port 80.

So in our case, we would run the below command.

`docker run simple-nginx -p 8000:80`

Once this command is run, we can connect to the web-server in our container by navigating to `http://localhost:8000` in our browser, and then see our website hosted!

docker commit
-------------

`docker commit` is used to create a new image from a customised container. It is quite similar to the git `commit`, in that it adds changes to a base image.  
 To see `docker commit` in action, let's use our customised NGINX base image.  
 * Run a container using the `simple-nginx` image and name it `new_nginx`.  
 * To commit the changes added in `simple-nginx`, run `docker commit new_nginx <dockerhub username>/first_commit`. The username is optional, only if you intend to add it to DockerHub.

docker push.
------------

The prerequisite to trying this command out is a DockerHub account.  
 `pushing` an image is once again, the Docker equivalent of git `push`, with the image being pushed as a repository to your DockerHub account or to another Docker registry.

To push an image, run `docker push <dockerhub username>/first_commit`.

The default tag given is the `:latest` tag. To optionally change it, add to the above command as follows: `docker push <dockerhub username>/first_commit:v2`. Here, `v2` is the new tag added.

The syntax for our push is therefore,  
 `docker push <dockerhub username>/<image name>:tag`

Go to your account and see your first image!
