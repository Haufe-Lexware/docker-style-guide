Ground Rules
============

Haufe Docker-Toolset
--------------------
There's already a plethora of tools around Docker and it is hard to define what will be the best option in the future.

For the time being, using Docker at Haufe asks for sticking to the "roots", so we don't waste time and effort in short-lived hypes or workarounds that do more harm than good.

The somewhat reduced "official" toolset consists of

  * docker
  * docker-compose
  * docker-machine
  * docker-swarm
  * git (optional)

For all of these tools you will will provide some Best Practices and/or Security Informations.


Docker for dev/test/live
------------------------------
Despite the involved tool-chains or stacks, Docker is basically a RUNTIME system and
has to adhere to *all* requirements and regulations of "Operations/IT/Security".

One of the consequences is the treatment of Docker-artifacts as "code": Versioned,
reviewed, verified, autobuilt and -tested and finally deployed into the designated environments.

---

[Guidelines](Guidelines)  
[Docker Docs - Home](../wiki/Home)  
