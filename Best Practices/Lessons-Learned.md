Lessons Learned
===============


Docker is easy, Dockerfile(s) not so much ...
---------------------------------------------------------
While working on your local machine with docker is "easy as pie". When you start working with "remote" locations (the usual scenario when your docker-host is running elsewhere - like "on azure") things start to get interesting:

* Beware of proxy requirements
	The command 

		yum update

	might work without problem on your (local) machine. But when you use a remote dockerhost (that might happen if you execute a docker-compose build), the settings might differ.

* Look out for name resolution issues
	the Docker configuration file "/etc/default/docker" show "--dns x.x.x.x" entries that CAN be of use, but sometimes make things worse. So just try first if the setting is REALLY necessary.

	Simply do sth like this:

		root@ra:~# docker run -it centos:5.11 bash
		[root@6753f0d41a1a /]# nslookup www.heise.de
		Server:		10.12.1.147
		Address:	10.12.1.147#53

		Non-authoritative answer:
		Name:	www.heise.de
		Address: 193.99.144.85
	
		[root@6753f0d41a1a /]# exit


Private "insecure" repositories
-------------------------------

When working with eval $(docker-machine env <machine-id>), remember that problems
with "insecure repositories" are not (only) located on the machine docker-compose
is running on, but on the "remote docker host" as well.

So if your docker login, docker-compose build etc. give you headaches because of
invalid certs and asks you to enter --insecure-repository entries or to place the
CA-certs to /etc/docker/... , then DO it on both/all machines.

Hint: Some commercial certificates are accompanied by Intermediat CA-certs.
In that case, place those certs to the /etc/docke/... directory.


Using "manual installed" docker-hosts
--------------------------------------
By default, the docker service will listen on unix:///var/run/docker.sock to allow only local connections by the root user. (See https://docs.docker.com/articles/basics/#bind-docker-to-another-hostport-or-a-unix-socket )

If you want to access such a machine via "tcp://..." like its done with docker-machine, you have to add/open the designated port by adjusting the file "/etc/default/docker".

	#DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"
	DOCKER_OPTS="$DOCKER_OPTS --host=unix:///var/run/docker.sock --host=tcp://0.0.0.0:2376"


An example of a "real world" configuration (boldly stolen from an docker-machine generated instance on azure) ...

	#DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"
	DOCKER_OPTS="$DOCKER_OPTS --tlsverify --tlscacert=/etc/docker/ca.pem --tlskey=/etc/docker/server-key.pem --tlscert=/etc/docker/server.pem --label=provider=azure --host=unix:///var/run/docker.sock --host=tcp://0.0.0.0:2376"


Because there WILL be some problems with certificates and such, sometimes (for a limited time, though ;-)) one can use an unsecured connection by setting DOCKER_TLS_VERIFY to an EMPTY STRING

	DOCKER_TLS_VERIFY=

[to be continued ...]

---

[Best Practices](Best Practices)  
[Docker Docs - Home](../wiki/Home)  
