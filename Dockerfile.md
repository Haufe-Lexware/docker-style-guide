# Dockerfile

A Dockerfile defines the contents of a [Docker Image](DockerImage.md) and is the main input for [Docker Engine](DockerEngine.md) when a `docker build ...` is executed.

## NO "upgrade" in NON-OS-Base-Images

While you **MAY** "update" the file-lists of the package manager of the OS in the **Base Image** you have chosen, you **MUST NOT** alter the contents of a **Base Image** by "upgrading" it in a Dockerfile build.

This is OK

	FROM ubuntu: 14.04.1
	RUN apt-get update \
		&& apt-get install -y ...
	# ...

This is BAD

	FROM ubuntu: 14.04.1
	RUN apt-get update \
		&& apt-get upgrade -y
		&& apt-get install -y ...
	# ...

The `apt-get upgrade` (or the command that does the trick in "your" **Base Image**) might change installed software versions or even install or remove packages based on new dependencies. The resulting Docker Image does NOT match the **Base Image** anymore.

If you NEED such statements because the `docker build` fails, **ASK** for a new **upgraded Base Image**


## INSIDE a Dockerfile, do NOT use puppet, ansible, salt, ...

You **MUST NOT** use configuration management tools (puppet, ansible, chef, ...) **INSIDE** a Dockerfile.

According to the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) a Dockerfile

> [...] is a text document that contains **all** the commands a user could **call on the command line** to assemble an image.

If you would use a configuration management tool inside the container,
you would still adhere to the recommendation, but violate it's intention.

1. You are going to install software packages and services(!) that are UNNECESSARY or risky at runtime (a database does NOT require puppet to be available).
2. The performed installation steps are HIDDEN from anybody who only has the Dockerfile
3. Most Dockerfile authors know the package management (apt, apk, yum, etc.) of the distribution being used as base of the Dockerfile, but not necessarily the config management tools.

## Use only well maintained images FROM a trusted registry

It is easy and convenient to download (pull) and use prebuild
images from or other public registries.

Because there is still the risk of poorly created or abandoned images, for non-experimental deployments, you **MUST** only use **official** Docker Images from the **Docker Hub** at [https://hub.docker.com/](https://hub.docker.com/) or from Haufe's own registry [https://registry.haufe.io/](https://registry.haufe.io).

> For the Haufe registry, you will only see some "nginx welcome page" at the moment, because it's behind a reverse proxy based on ... nginx ;-).

Sample Dockerfile for **Docker Hub**

	# official image, because there is NO account or the "library" account being used
	FROM ubuntu:14.04.1
	# FROM library/ubuntu:14.04.1
	# FROM hub.docker.com/library/ubuntu:14.04.1

Sample Dockerfile for **Haufe's Registry**

	# Haufe image
	FROM registry.haufe.io/hgg/openam:latest

**PUSHing Docker Images TO Haufe's registry is limited to autobuild (technical) users. If you want to have your images autobuild or need pushing permissions for your project, contact Release Engineering (first ) or the CTO Team.**

## NO secrets in Dockerfile (or its repository)

A VERY bad example of a Dockerfile would be

	FROM ubuntu:14.04.1
	MAINTAINER ...
	ENV API_KEY=4711101 \
		USR=admin \
		PWD=the_admin_password \
		CREDITCARD=5555 3333 2222
	ADD the_same_secrets.txt /etc
	# ...

You **MUST** keep secrets out of the services Dockerfile **AND** its repository.

Dockerfile repositories with all their accompanying files tend to be cloned,
shared, etc. IF you forget about the secrets inside, anybody who gains access
to the repository would immediately KNOW your precious secrets.

You can solve this dilemma by
- provide secrets as **environment variables** when you start the container with `docker run -e API_KEY=4711 ...`
- create strictly **separate repositories for secret/configuration containers**
	that are NEVER at risk being published outside
- create configuration only **containers "on the fly"** during provisioning
- let the **containers entrypoint or command retrieve secrets** at startup.


## VERIFY downloaded artifacts

When using the Dockerfile with the `docker build` command, files from the local filesystem (the build context) can be used or being retrieved from services in the intra- or internet.

You **MUST** verify externally downloaded files. 


### VERIFY downloaded artifacts (I)

You **SHOULD** use one of: 

- a signature for the external file itself
- a signed file with the HASH for the external file and the signing key from a public keyserver. 

> Using a keyserver with HTTP support (port 80) might help with problematic firewalls.

     # ...
    ENV HASHICORP_KEYIDS=51852D87348FFC4C
     # ...
	RUN curl -sL https://releases.hashicorp.com/vault/0.5.0/vault_0.5.0_linux_amd64.zip >  vault_0.5.0_linux_amd64.zip \
        && curl -sL https://releases.hashicorp.com/vault/0.5.0/vault_0.5.0_SHA256SUMS > app.sha \
        && curl -sL https://releases.hashicorp.com/vault/0.5.0/vault_0.5.0_SHA256SUMS.sig > app.sig \
        && gpg --keyserver http://pool.sks-keyservers.net:80 --recv-keys ${HASHICORP_KEYIDS} \
        && gpg --verify app.sig app.sha \
        && grep linux_amd64 app.sha | sha256sum -sc \
        && echo "We only get here if sha256sum succeeded ..."


### VERIFY downloaded artifacts (II)

If there is no better option, you **SHOULD** use a well known HASH from a trusted source (e.g. placed directly in the Dockerfile)

     # ...
	ENV VAULT_SHA256=f81accce15313881b8d53b039daf090398b2204b1154f821a863438ca2e5d570
     # ...
    RUN curl -sL https://releases.hashicorp.com/vault/0.5.0/vault_0.5.0_linux_amd64.zip > /tmp/my_file \
        && echo "${VAULT_SHA256}  /tmp/my_file" | sha256sum -sc  \
        && echo "We only get here if sha256sum succeeded ..."


## No "root" processes in containers (please)

A process inside a container **SHOULD NOT** run as root (with uid “0”) to reduce possible runtime risks - especially in respect to (root-owned ?) volumes from the host. Even a Docker Engine > 1.10 (with new security features enabled) is a misconfiguration risk to be avoided.

If possible, set the effective runtime-user in the dockerfile.

    host$ cat dockerfile
    FROM ubuntu

    # Installing as almighty "root"
    RUN ...
    COPY ...

    # now switching to harmless "guest" runtime user
    USER guest

    ENTRYPOINT ["/my_entrypoint.sh"]
    CMD ["/my_command.sh"]

> Some programs - like Apache or Nginx - have to be **STARTED** as root,
but provide configuration settings to switch to a different, much less
risky runtime user.

## Only EXPOSE necessary ports

In a Dockerfile, you **MUST** only `EXPOSE` ports that are required
from outside of the container. If a program provides its API via
port 80 AND 443, but you don't really need port 80, this should be
reflected in the Dockerfile:

	 #
    ADD ...
    
     # Disabled
     # EXPOSE 80
    
     #
    EXPOSE 443


## Write Log/Error to Stdout/Stderr

The Docker Daemon stores or forwards data (text-strings) that is written to stdout or stderr
by the started process inside a container. The container **MUST** use this functionality **IF POSSIBLE**
to support a standardized log management approach.

Stdout **SHOULD** contain regular information
about the process doings, while stderr **SHOULD** be restricted to messages about technical errors
or warnings that an operator or admin has to take care of.

Such messages **SHOULD** be machine readable (e.g. json formatted) to avoid extensive parsing steps in later processing.

Of course, the application **MAY** uses other (additional) means of log
forwarding but is immediately on its own for maintenance, configuration etc.

## Use Exec form rather than Shell

You **MUST** write [CMD](https://docs.docker.com/engine/reference/builder/#cmd) and [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) statements using the Exec-form.
Using the shell form would effectively trigger a call to `/bin/sh -c` with the command and parameters you specified. 

As a result, when you use `docker stop` or `docker kill` the POSIX signal will only be sent to the container process running as PID 1, and if that process is /bin/sh rather than the underlying process you started and /bin/sh doesn't forward signals to any child processes you won't be able to [gracefully stop the process](https://www.ctl.io/developers/blog/post/gracefully-stopping-docker-containers/).

## One Process/Service per Container

A Dockerfile **MUST** only install packages for ONE **logical** service.

A logical service **SHOULD** be only a **SINGLE** process like one
web- or database server.

	FROM ubuntu:14.04.1
	CMD [ "/opt/myservice/myprogram" ]

The technical reason is the STREAMS (Stdin/Stdout/Stderr) and SIGNAL handling between the Docker Engine and
the process(es) running in a Docker Container. When not constructed/handled
carefully, something similar to "unix process zombies" might raise their
ugly heads ...

This asks for installing and starting applications the "right way"

> There are solutions for cleanly handling multiple processes inside a
> container like [Using Supervisor with Docker](https://docs.docker.com/engine/admin/using_supervisord/),

