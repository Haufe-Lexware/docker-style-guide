# Setting up your local machine to develop Docker

So what you have seen so far are the basic docker tools that you may use here at Haufe Group. What you have hopefully also noticed is that there is a tooling progression that makes using docker more efficient and speeds up development with Docker the higher-up you go on the toolchain.

Docker can help you with the setup of your dev environment. Docker enables you to find and coordinate application dependencies faster. At the same time, by choosing to use Docker, you also have to ensure that your application runs the way you intend it to inside the Docker container.

## Prerequisite \#1: Debugging your app "in container"

So, you installed Docker, worked with the tools - albeit in kind of an uncomfortable way, and now, you want to start developing your application with Docker in your favorite IDE that supports your technology of choice. That's awesome, but you must be able to debug your application inside of the container to ensure that you have everything you need in the application environment.

By debugging, we don't mean debugging your code because you do this in your IDE. We mean ensuring that your application has everything that it needs to run in the container. One of your targets here is to create an immutable running application environment and to configure this environment.

### Docker and your favorite IDE

IDE support for Docker is being extended every day because the major IDE providers realize the importance of container technologies, and so, it can be that native IDE support for "debugging all applications from inside all Docker containers" is available soon. This level of debugging coverage is not available right now though - so there are essentially two ways to debug a Docker container:

* Debug using a Docker Container that runs your IDE
* Debug using remote debugging

### Debug from inside your container

For getting started this technique may be the easiest way to debug your docker app. This is a proven way to debug, and Docker makes this easy by providing ready-to-pull Docker images in Docker Hub. Requirements for doing it this way are:

* You must mount your code into the container
* You must be able to have a GUI view of your container by using x11 vnc protocol or some other way to view it graphically. Usually instructions for this are on Docker Hub

The downside here is that, since your container runs your IDE, it is not a production-ready container. You must not deploy this container.

Another potential downside is that you could potentially delete your code if you mount files from your hard drive. You can mitigate against this by committing to git and initializing and cloning your code into your containers working directory, doing a rebase on subsequent run commands and so on.

There are images in Docker Hub for many well known IDEs including VS Code, Intellij, NetBeans, Eclipse and even more IDEs. We are optimistic about these dockerized IDEs:

* [Visual Studio Code](https://hub.docker.com/r/jess/vscode/)
* [Intellij](https://hub.docker.com/r/psharkey/novnc/)

Instructions on how to install these images are in the descriptions on Docker Hub.

### Remote Debugging

For a production development and maybe for startup development, setting up Docker container remote debugging is more effective. Remote debugging can be defined and placing debugging components in your Docker container so the container can communicate debugging data with your IDE.  This is already partially supported by some IDEs. One example of remote debugging is that you can add docker support and debug  the container in Visual Studio for .NET Core projects.

This is more effective because, if you set up remote debugging correctly, your local container dev environment is closer to the same configuration as a production container environment. This topic can be complex since  each IDE and each technology is different. Just to provide an example, here is a short tutorial on [how to configure VSCODE to remote debug dockerized NodeJS applications](https://alexanderzeitler.com/articles/debugging-a-nodejs-es6-application-in-a-docker-container-using-visual-studio-code/).

To get this to work on my machine, I had to make a few changes to the Dockerfile and the VSCode Launch.js debug config. These changes are [here](https://github.com/SSpeights/docker-style-guide/tree/master/examples/VSCode_RemoteDebugContainer_NodeJSEnv).

## Prerequisite \#2: Also create a production environment

Once you have a working dev environment you still also need to set up a production environment that doesn't contain any IDE or active remote debugging components. This is still essential to ensure that your application works correctly. In the case of the Node tutorial, you would create a Node image that does not activate the debugger utility.

