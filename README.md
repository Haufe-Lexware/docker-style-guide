# Why does Haufe need it's own docker book

I don't really know if it's fair to call this a book. I think it's probably better to call it a Docker frame or  something similar. Fact is, there is a lot of Docker documentation out on the net and also some official Haufe documentation - like our Docker Style Guide. So, the purpose of this "Docker frame" is to frame useful content for Haufe developers, release engineers, runtime operators, and anyone else like you, who are going to use Docker on a regular basis, into a relevant context.

This context should provide you with things like:

* A human-readable organization, so you can find Docker knowledge that you must have fast\(er\)
* Recommendations on how you should learn Docker
* Cool links to Docker documentation that fits to what you are doing with Docker
* Some Haufe-unique tips on how to do stuff like get around our fantastic firewall and proxy server

Hopefully, the Haufe Group Docker book can provide you with a good frame of reference to get started with Docker and help you progress up to automatically building and deploying composed, scalable, dockerized applications over continuous delivery pipelines. It will take a while to put all of the information into this frame, and we, the folks who collaborate on this project, welcome your feedback over all channels, so we can make the information here better as we go.

## Organization: Frame of reference

This book is designed to help Haufe Group employees get started using Docker. The organization is taken from the "Next Best Action" project, where non-engineer employees were asked to create a small application in Docker.

In the first part of the book, the organization is designed, for employees, who have no experience with Docker and, who may not work regularly at developing software. The second part of the book, let's say from Docker Compose on-wards, gets into concepts that need to be supported by software developers. Keeping that in mind, and the fact that this book is really a framework, here is how you should use this book to learn Docker.

## How to use the Docker book

Our CTO asked me to create a rolling narrative for this book, meaning, that the book should provide a continuous story line for learning Docker. Since Docker has already been documented extremely well in other parts of the internet, much of this book is designed to point you to these links, so you can read about concepts and tutorials. After that you can come back to this book to continue with the next step of working with Docker.

To put it in plain English, the proposed way to use this book is to: read the book, follow the links, learn the concept or do the tutorial \(you can of course keep going\), but then come back to the book to move on to the next step. The book links not only official Docker docs but also to other third-party documentation and to Haufe Group Docker documentation that contains requirements for using Docker in production at Haufe Group. You will want to bookmark these links so you can access them when working on tutorials and, later, developing your own dockerized apps.

But, you also need to read the content of the book too. This Docker book contains previously undocumented information like how to work from behind of the Haufe Group proxy server or to understand why we want to use Docker at Haufe Group. Maybe not so much information as in an O'Reilly Media book, but still important if you want to use Docker locally on your dev machine to develop software.

## Contributing to Haufe Group's DockBook

If you are working with Docker in your spare time or for a Haufe Group project and feel like you have something to contribute, we want your input! Providing "real help" to people who want to learn Docker and maintaining this book are both very important for us, and the best way to do it is to leverage the knowledge of the entire Haufe Group Docker community. So, if you want to add an additional section or provide code samples to give people a hands-on idea how Docker principles work, we're all for it.

To help with the book go to the [Haufe Docker Style Guide GitHub repository](https://github.com/Haufe-Lexware/docker-style-guide) and fork it to your own GitHub account. Then, [Create a GitBook account](https://www.gitbook.com) and use your forked repository as the book content: You do this from the "GitHub" section in your book's "Settings". With GitBook, you can do everything from your browser, including editing the book. Alternatively, if you want, you can just fork the GitHub account and edit the markdown from a good editor like VS Code. When you have something new, make a pull request from your local repo.

Your changes will be reviewed and, if they add value, merged into the Haufe-Lexware Style Guide repository and published via our GitBook. If you, have any questions about any of this feel free to ask the Style Guide editors about forking, working with GitBook, or whatever other questions you may have.

Our style guide has a very simple structure:

* .md files in the master branch are the documentation. 
* Code samples go in the "examples" folder - pls create a separate, well-labeled folder for your example.

Hope to be getting pull requests for the Docker Style Guide soon!

# Table of contents

* [Why Docker](why_docker.md)
* [How docker works](how_docker_works.md)
* [Installing Docker](installing_docker.md)
* [Docker Basics](docker_basics.md)
* [Using Docker registries](using_docker_registries.md)
* [Creating base images with Docker CLI](creating_base_images_with_docker_cli.md)
* [Building your own images with Dockerfile](building_your_own_images_with_dockerfile.md)
* [Managing Docker host with Docker Machine](managing_docker_hosts_with_docker_machine.md)
* [Docker Compose](docker_compose.md)
* [Setting up your local machine to develop Docker applications](setting-up-your-local-machine-to-develop-docker-applications.md)
* [Building Docker images](building_docker_infrastructure_and_applications.md)
* [Glossary](GLOSSARY.md)



