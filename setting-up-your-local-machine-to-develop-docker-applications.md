## Setting up your local machine to develop Docker

Docker can help you with the setup of your dev environment. Docker enables you to find and coordinate application dependencies faster. At the same time, by choosing to use Docker, you also have to ensure that your application runs the way you intend it to inside the Docker container.

So, you installed Docker, worked with the tools - albeit in kind of an uncomfortable way, and now, you want to start developing your application with Docker in your favorite IDE that supports your technology of choice. That's awesome, but you must be able to debug your application inside of the container to ensure that you have everything you need in the application environment.

By debugging, we don't mean debugging your code because you do this in your IDE. We mean ensuring that your application has everything that it needs to run in the container. One of your targets here is to create an immutable running application environment and configuring this environment is one of your debug tasks.

IDE support for Docker is being extended every day because the major IDE makers realize the importance of container technologies, and so it can be that native IDE support for "debugging all applications from inside all Docker Containers" is available soon. This level of debugging coverage is not available right now though, so there are essentially two ways to debug a Docker container:

* Debug using a Docker Container runs your IDE
* Debug using remote debugging

### Debug from inside your container

For getting started this is the easiest way to debug your docker app. This is a proven way to debug, and Docker makes this easy by already having Docker images ready for you to pull in Docker Hub. Requirements for doing it this way are:

* You must mount your code into the container
* You must be able to have a GUI view of your container by using x11 vnc protocol. Usually instructions are on Docker Hub

The downside here is that, since your container runs your IDE, it is not a production-ready container. So, you may not deploy this container.

Another potential downside is that you could potentially delete your code if you mount files form your hard drive. You can mitigate against this by committing to git and cloning to your containers working directory.

There are images in Docker Hub for most of the IDES VS Code, Intellij, NetBeans, Eclipse and even more IDEs. We are optimistic about these dockerized IDEs:

* [Visual Studio Code](https://hub.docker.com/r/jess/vscode/)
* [Eclipse](https://hub.docker.com/r/psharkey/eclipse/)

### Remote Debugging

For a production development and mayb for advanced startup development, setting up Docker container remote debugging is more effective. Remote debugging can be defined and placing debugging components in your Docker container so the container can communicate debugging data with your IDE.  This is already partially supported by some IDEs. One example of remote debugging is that you can add docker support and debug  the container in Visual Studio for .NET Core projects. 



Set up a runtime container add remote debugger

Set remote debbuger to so the IDE and perform remote debugging

