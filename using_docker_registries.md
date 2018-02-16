## Searching Registries

When you begin with docker you should have a good idea what you want to do. This is where Docker's composability can help, and chances are, that there is already an image at the Docker Hub or in the Haufe Group Docker Registry, that already meets your needs. So let’s say you want to create a Web application. Then you probably need some kind of web server, you can pull down a docker image for Apache web server, Glassfish and just about any other kind of open source web server you can imagine. Docker enables you to push images to the other registries as well and even create your own private registry.

_ToDo: A note about security for using public images. _

### Docker Hub

There are several ways to look for images but the best way to find what’s out there is to go to [https://hub.docker.com/](https://hub.docker.com/) and search for what you need to build your application. You will also want to create a docker hub account – here you can store your personal images. Try this:

Go to Docker Hub and type in **"httpd"** in the search field. You should get a very long SERP of dockerized Apache Web Server images. Search for other well known software like node JS, MongoDB, FluentD, Ubuntu, and many others - you will find that all of this software has been dockerized into docker images and that, just like the software, these docker images are open source and free to use for your development purposes.

If you are looking for a tutorial to explore Docker Hub, [Step 4 of Roman Irani's Docker tutorial](https://rominirani.com/docker-tutorial-series-part-4-docker-hub-b51fb545dd8e#.kn7dpyu9t) is pretty good.

### Finding images with your CLI

You can also search for images from the command line by using the “[docker search](https://docs.docker.com/engine/reference/commandline/search/)” command. But, the documentation at docker hub is in my opinion, more human-readable: i.e. if you don’t know exactly what you want, you’ll be able to research better and figure out if you need it or not on Docker hub.

Browse for software that interests you.

By seeing what's already on docker hub, you can get a feeling for how wide-spread docker has become and how much easier it is with docker to compose portable applications that take up very few resources.

**Achtung:** There is a new docker registry called the [Docker Store](https://store.docker.com/), which looks like it is slowly replacing the Docker Hub. You may also want to add this as on of your Docker bookmarks.

### Create a Docker ID

Once you are done exploring what's there, you want to create your own [Docker ID and Docker Hub account](https://hub.docker.com/) this is your docker sandbox for customized images. Once you have configured your image locally, you can [push it up to Docker hub](https://docs.docker.com/engine/getstarted/step_six/) and make it publicly available.

### Haufe Group Docker Registry

Once you have explored the Docker Hub you will also want to take a look at the Haufe Group Docker Registry located at registry.haufe.io and even [create your own private registry](https://docs.docker.com/registry/). Her is the [cheat sheet version to create your own Docker registry](http://docker.jens-piegsa.com/#private-docker-registry).

You can browse the Haufe Group registry by opening your favorite shell and typing:

`docker search registry.haufe.io/*`

### Section targets

Now that you are done with this section you should be able to:

* Search the Docker Hub for interesting images
* Have your own Docker Hub account
* Search through the Haufe Group Docker registry
* Know how to find what you're are looking for in Docker regsitries \(Docker Hub and Haufe Group Docker Registry\) to ease setting up your application environment.



