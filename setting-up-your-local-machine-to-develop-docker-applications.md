## Setting up your local machine to develop Docker

So you have installed Docker, worked with the tools albeit in kind of an uncomfortable way, and now you want to get started developing your application in your favorite IDE that supports the technology you select. We encourage you do this of course, but you must be able to debug your container.

  
IDE support for Docker is being extended every day because the major IDE makers realize the importance of container technologies, and so it can be that native IDE support for "debugging all applications from inside all Docker Containers" is available soon. This level of debugging coverage is not available right now though, so there are essentially two ways to debug a Docker container:

* Debug using a Docker Container runs your IDE
* Debug using remote debugging

### Debug from inside your container

To get started this my be the easiest way to debug your docker app

* This where you create a container with your app and with your IDE

Git Clone instead of mount.

Use x11 to display your IDE

There are images in Docker Hub for most of the IDES VS Code, Intellij, NetBeans, Eclipse

Eclipse good

NetBeans not so easy to display

VSCode good

Do not deoply

### Remote Debugging

Set up your container so that it connects to your IDE

Test this with Visual Studio and .NETCore

Set up a runtime container add remote debugger

Set remote debbuger to so the IDE and perform remote debbuging

