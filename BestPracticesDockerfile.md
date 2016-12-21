# Best practices - Dockerfile

## One Dockerfile Per Source Repository

While it is tempting to put any Dockerfile of a project in a single repository to build all **Docker images** at once, you **SHOULD** keep each Dockerfile \(and its resources\) separate.  
For autobuilds \(gocd, jenkins, ...\), it is **essential** to monitor changes of a repository for **one** Dockerimage and start builds with clearly defined dependencies.

## Start "interactive"

You can just write your Dockerfile...

```
$ cat Dockerfile
FROM ubuntu:14.04
RUN curl -sL https://github.com/hlgr360/docker-templates/archive/master.zip \
  -o /tmp/master.zip
```

and test it ...

```
$ docker build .
Sending build context to Docker daemon 2.048 kB
Step 1 : FROM ubuntu:14.04
 ---> 14b59d36bae0
Step 2 : RUN curl -sL https://github.com/hlgr360/docker-templates/archive/master.zip   -o /tmp/master.zip
 ---> Running in 5c9deb4eb14a
/bin/sh: 1: curl: not found
The command '/bin/sh -c curl -sL https://github.com/hlgr360/docker-templates/archive/master.zip   -o /tmp/master.zip' returned a non-zero code: 127
```

alter the Dockerfile, retest ... etc.

It is easier, to start the intended **Base Image** in interactive mode and just "do" the installation steps and take notes what works \(and what not\).

```
root@10f5608e9db3:/# curl -sL  https://github.com/hlgr360/docker-templates/archive/master.zip   -o /tmp/master.zip
bash: curl: command not found
root@10f5608e9db3:/# apt-get update && apt-get install -y curl
Ign http://archive.ubuntu.com trusty InRelease
Get:1 http://archive.ubuntu.com trusty-updates InRelease [65.9 kB]
[...]
Setting up curl (7.35.0-1ubuntu2.6) ...
Processing triggers for libc-bin (2.19-0ubuntu6.7) ...
Processing triggers for ca-certificates (20160104ubuntu0.14.04.1) ...
Updating certificates in /etc/ssl/certs... 173 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d....done.
root@10f5608e9db3:/# curl -sL  https://github.com/hlgr360/docker-templates/archive/master.zip   -o /tmp/master.zip
root@10f5608e9db3:/#
```

## Reduce the number of Layers

Almost all statements in a Dockerfile create additional layers for the Dockerimage while running `docker build`. If you concatenate those statements, the image can be optimized:

Instead of

```
FROM debian:wheezy
WORKDIR /tmp

ENV TEST1 1
ENV TEST2 2

RUN wget -nv
RUN tar -xvf someutility-v1.0.0.tar.gz
RUN mv /tmp/someutility-v1.0.0/someutil /usr/bin/someutil
RUN rm -rf /tmp/someutility-v1.0.0
RUN rm /tmp/someutility-v1.0.0.tar.gz
```

You should create

```
FROM debian:wheezy
WORKDIR /tmp

ENV TEST1=1 \
    TEST2=2

RUN wget -nv && tar -xvf someutility-v1.0.0.tar.gz
  && mv /tmp/someutility-v1.0.0/someutil /usr/bin/someutil
  && rm -rf /tmp/someutility-v1.0.0
  && rm /tmp/someutility-v1.0.0.tar.gz
```

The resulting image has fewer layers and therefore takes up less space than the first example.

## Package installation first

When adding files "work in progress" from your local build context, long running Dockerfile statements should be placed first, so the build cache can be effective.

BAD - any change to files in your `./root` directory tree will invalidate the build cache and trigger a new execution of `apk --update...`.

```
# Add changed files from context
ADD root /

# Update package information, install packages and clear package cache
RUN apk --update add curl ca-certificates gnupg jq \
&& rm -rf /var/cache/apk/* 
```

OK - most likely, the cached result of `apk --update...` will not change any time soon. Changes to files in your `./root` directory tree will only lead to a new "quick" layer update for the changed local files.

```
# Update package information, install packages and clear package cache
RUN apk --update add curl ca-certificates gnupg jq \
&& rm -rf /var/cache/apk/* 

# Add changed files from context
ADD root /
```

## DON'T USE ADD with URLs!

The following disables caching of subsequent Docker statements.

```
ADD https://.../filename /tmp/filename
# not using cache anymore :-(
```

Better use curl or wget \(whatever is available\)

```
RUN curl -L https://.../filename > /tmp/filename
# caching still in effect :-)
```

## Add \(multiple\) files via structured directory

Usually, you would add files by ADD similar like this

```
ADD file1.txt /some/path1/file1.txt
ADD file2.txt /some/path2/
ADD file3.txt /some/other/path3/
```

The same result can be achieved \(easier\) by using a subdirectory structure available in the build-context. Example file listing

```
host$ find .
.
./root
./root/etc
./root/etc/vault
./root/etc/vault/vault.json
./root/entrypoint.sh
./Dockerfile
host$ cat Dockerfile
FROM ubuntu
# Add all files from a directory structure
ADD root /
# The image now contains /etc/vault/vault.json AND /entrypoint.sh
```

## Set correct file permissions outside the Dockerfile

This is BAD, because it takes time and creates a new layer:

```
host$ cat Dockerfile
FROM ubuntu
# creates one layer
ADD entrypoint.sh /
# creates another layer
RUN chmod +x /entrypoint.sh
```

This is OK:

```
host$ chmod +x entrypoint.sh
host$ cat Dockerfile
FROM ubuntu
# creates one layer and preserves the (already set) execution flag
ADD entrypoint.sh /
```

## Entrypoint vs CMD {#entrypoint-vs-cmd}

You **SHOULD** use Entrypoint to specify the default executable that will be called when a container is started and the default arguments that you want to be easily overridable should be provided via CMD.

More in depth explanations can be found [here](https://www.ctl.io/developers/blog/post/dockerfile-entrypoint-vs-cmd/)

