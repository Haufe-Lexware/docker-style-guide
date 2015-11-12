#Puppet, Ansible, etc. vs. Dockerfile


## This is a simple "discussion" how you should "see" your Dockerfile in respect to other formas of installation and/or configuration approach.

### Question:

[...] As an example, we have shell scripts for deploying a project. You could basically just write the necessary commands in the Dockerfile to copy over all the sh scripts and then run them same thing that an Application Operations colleague would do or should we minimize the dockerfile to only the "infrastructure" needed and then deploy with Ansible?

or should we have as little as possible in the dockerfile and everything needed should be in ansible for example, so that you are not locked-in into docker and can reuse those automation scripts to deploy to cloud, dev machines or docker or anywhere else for that matter? [...]

### Answer:

As  configuration tools like Ansible, Chef, ... are for managing servers (virtual or physical), they don't fit quite to a Dockerfile ...
1. You would have to insert the necessary clients
2. They are somewhat like "black magic" (ruby programming and such) and are sometimes a huge effort in themselves (remember the rather complex puppet script for the umantis tools ...)
3. They are meant to be portable/compatible to different systems whereas the Dockerfile defines ONE environment and nothing more
4. configuration tools like puppet control services by verifying the availability, version, run state etc. for services and programs to shut them down controlled in case of updates/modifications and start them up after configuration is done. And that is done on the running machine (not in the container being created)

Dockerfiles are a description of ONE specific config. There's no need for the Dockerfile to be configurable after creation beside runtime informations that have to be provided by environment variables (example: API-keys, user-names, ...).

All the configuration and automation tools play a huge role in automating the docker build and deplyoment processes, even for ramping up the docker services themselves. For the Dockerfiles, I'd go for "pure" OS-specifc commands, like apt-get, yum, etc.

---

[Best Practices](Best Practices)  
[Docker Docs - Home](../wiki/Home)  
