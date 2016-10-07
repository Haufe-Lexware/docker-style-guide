# Best Practices - Container

## Data only container

The creation and the usage of Data only containers can be found in the paragraph [Creating and mounting a data volume container](https://docs.docker.com/engine/userguide/containers/dockervolumes/).

Basically, a Data only container is a container with an immediatly exiting command or entrypoint. It provides one or more `VOLUME`s (aka directories or files) for modification to other containers.

A `VOLUME` **MAY** be defined in the Docker Image,

	$ cat Dockerfile
	FROM ...
	VOLUME ["/var/data"]

but it **SHOULD** be defined at runtime with docker create or run

	$ docker create -v /data --name dbstore ubuntu:14.04.1 /bin/true

or with docker-compose

	$cat docker-compose.yml
	data:
		image: ubuntu: 14.04.1
		command: /bin/true
		volumes:
		- "/data"

## Log Forwarding

In [Dockerfile](Dockerfile.md), it is being said to [Write Log/Error to Stdout/Stderr](Dockerfile.md#write-logerror-to-stdoutstderr).

Log information ends up in a JSON formatted log file (two for each **Docker Container**). Until recently, you would have to take care of forwarding the logs completely by yourself. One (still) acceptable solution was to use a container with a log monitoring/forwarding application inside, for example [fluentd](http://www.fluentd.org/).

Since Docker 1.9, you can use [Log Drivers](https://docs.docker.com/engine/admin/logging/overview/) to skip the step of writing the JSON logs, reading/parsing them and forward the content.

But, if you use the [Fluentd](https://docs.docker.com/engine/admin/logging/fluentd/) approach,
you have still the need for a **Fluentd Container** that acts as an encrypting proxy.
Out of security reasons, you are not allowed to send UNENCRYPTED log data (with possibly sensible content) to a log receiver on a different host.
You **MUST** use the [Secure Forward plugin](http://docs.fluentd.org/articles/out_secure_forward) to have a TLS enabled connection.

By default the log messages will be passed to a fluentd instance listening on localhost:24224, if you need to customize that you can use the log driver option [fluentd-address](https://docs.docker.com/engine/admin/logging/fluentd/#fluentd-address).

By default log messages are tagged using the first 12 chars from the Docker container id, customization of tags is explained [here](https://docs.docker.com/engine/admin/logging/log_tags/).

To ensure no messages are lost you **SHOULD** configure the secure_forward plugin to use [file buffering](http://docs.fluentd.org/articles/out_secure_forward#buffered-output-parameters) rather than the default in-memory buffer.

## Container - "readiness"

A container is an entity that can be used "out of the box". You wouldn't expect additional "preparation" steps or long-lasting "warm-up" phases.
A Docker container should be ready to start "at an instant", with only "parameters" for "personalization". An example would be some web-server that is started with the server-hostname as a parameter.

## Container are ephermal

Expect the **Docker Container** instance to be destroyed and restarted as/in a NEW instance at ANY time.

As a consequence, it's best to make your services stateless

## Create small images because of deployment/image transfer

There is some race to create the smallest Docker Images possible,
but it is important to remember, that only the **Docker Image** hogs the space
on your harddisk and not the **Docker Container**.
The containers will only occupy the differences to the image.

## Using identical (base) images for service and data only container

This is not about size, but about using the IDENTICAL UID/GID in
two containers without special preparation. If you are going to "mount" a directory from a
different container by using `VOLUME`'s, you should really think about using (at least) the identical images for service
and data container to prevent mismatching UID/GID between the two.
