#Creating a Dockerfile almost interactivly

## Ready ...
Usually, you start a Dockerfile by entering the baseimage information, some Dockefile commands and then check if everything works with

``` text
    $ docker build .
```

You'll use the output of the process to adjust the Dockerfile and retest ... and retest ... and retest ...


## Steady ...

Better use a bash (or sh) "inside" the base image and make EXACT notes in the Dockerfile what had to be done.

For example, you want to download a file inside an Ubuntu 14.04.2 image:

``` dockerfile
FROM ubuntu:14.04.2
RUN curl -L https://github.com/hlgr360/docker-templates/archive/master.zip \
  -o /tmp/master.zip
```

This would show an error, you have to find out what to put in the Dockerfile and then (guess what?) retest ...

``` dockerfile
FROM ubuntu:14.04.2
RUN apt-get update && apt-get install -y curl
RUN curl -L https://github.com/hlgr360/docker-templates/archive/master.zip \
  -o /tmp/master.zip
```

## Go!

That works quite well for a SMALL number of commands. But if you have a dockerfile with a large number of commands, you'll be better off by doing it interactivly

``` text
$ docker run -it ubuntu:14.04.2 bash
root@67269163407c:/# curl -L \
 https://github.com/hlgr360/docker-templates/archive/master.zip \
  -o /tmp/master.zip
bash: curl: command not found
root@67269163407c:/# apt-get update && apt-get install -y curl
[...]
Processing triggers for libc-bin (2.19-0ubuntu6.6) ...
Processing triggers for ca-certificates (20141019ubuntu0.14.04.1) ...
Updating certificates in /etc/ssl/certs... 173 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d....done.
root@67269163407c:/# curl -L \
 https://github.com/hlgr360/docker-templates/archive/master.zip \
  -o /tmp/master.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   129    0   129    0     0    271      0 --:--:-- --:--:-- --:--:--   271
  0     0    0 49414    0     0  39990      0 --:--:--  0:00:01 --:--:-- 39990
root@67269163407c:/#
```

---

