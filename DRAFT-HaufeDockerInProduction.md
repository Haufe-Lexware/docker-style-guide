![](images/draft.png)

# Docker in production

![](images/docker-logo.png)

The decision to use Docker containers **internally** for products or services can be made by the product/service teams themselves.

If Docker becomes an integral part of a **publicly available** system or service , there are some additional requirements to be met.

## Docker Host

A Docker Host is a **physical or virtual machine** with an operating system and a running docker-engine. 

The service(s)/application(s) inside the container **MUST** consider [Secure Development Rules](http://group/websites/ia/DokumenteOeffentlich/Secure%20Development%20Rules.pdf)

The **Dockerhost** as an IT-System **MUST** follow [Haufe - 10 Rules for Secure Server Operations V1.0](http://group/websites/ia/DokumenteOeffentlich/Haufe%20-%2010%20Rules%20for%20Secure%20Server%20Operations%20V1.0.pdf)

If your **Docker Image/Container** is based on some OS-Distribution (Debian/Centos,Windows,etc.), you **SHOULD** treat it like an IT-system, too.  

Here are additions to the Rules for Secure Server Operations based on Docker considerations:

### 1. Hardening

In addition to the usual OS hardening, follow https://benchmarks.cisecurity.org/tools2/docker/CIS_Docker_1.6_Benchmark_v1.0.0.pdf

### 2. Logging

A **Docker Host** (Host-OS and Docker-Engine) and any Docker-Container on a Docker-Host **MUST** provide their log-information or metrics to the (upcoming) central Haufe log-management system (graylog).

The container **SHOULD** log to **stdout/stderr** and use the Docker-fluentd-log-driver to forward the logs to a (fluentd) log-proxy to take care of the central log requirement.

### 3. Patch-Management

The **Docker Host** **MUST** be integrated in the patch-management process. The **Docker Host** **SHOULD** be patched by using newly created **Immutable (Host) servers** and **Blue/Green depoyment ** instead of updating installed software.

### 4. Monitoring

The **Docker Host** must be monitored as well as the **Docker Containers** (better: The processes running inside) running on a **Docker Host**. It's crucial to identify malfunctioning processes inside a container or host metrics that could have a (negative) impact on each container running on the host.

### 5. Backup

A **Docker Host** should be treated as an identically re-creatable unit and does not require specific backup processes. For **Docker Containers** creating/using persistent data, either consider using data-storage solutions/services or use other available (remote) backup approaches (DB-backup, ...). You **MUST** not use the **Docker Host** as a backup medium, because the Host might "vanish" at any time (e.g. Update, Failure, Migration, ...)

### 6. Virtualize (the right way ...)

See "Secure Server Operations :-)"

### 7. Malware

> It's an open topic if (and how to) Antivirus software MUST/SHOULD/MAY be installed on the **Docker Host** or inside the **Docker Image/Container**. 
> 
> IF any component would be immutable/read only EXCEPT the persistent/persisted data, it doesn't seem to be necessary if it could be verified that the installation wasn't compromised.

### 8. Remote access

#### Docker Host

For OS/Docker installation/operation purposes, the Dockerhost **MUST** provide access by public/private key (ssh). Using the **Docker Engine** from remote, bi-directional authentication and encryption by using certificates (TLS) **MUST** be enabled.

#### Container

You **MUST NOT** install any telnet/ssh/... service inside a Docker container **except** it is the intended function/service of the container itself. E.g. there is no need to install a sshd inside a **Docker Image** that provides a Tomcat app-server.

### 9. Security structures

The placement of the **Docker Hosts** in/to the right (virtual) networks/segments is a given. You **MUST** restrict network traffic to/from **Docker Containers** with the help of the **ports** statement in docker-compose (or  with `docker run -p, --publish=[]`). You **SHOULD** limit communication between containers by using **Docker Networks** if possible (Docker >= 1.10).

### 10. Security processes

You **MUST** adhere to company regulations for **Docker Containers** like you would for any service that is presented to the public.


## Docker Engine

Because of (expected/required) security features (user namespace mapping, AppSec functionality, authorization plugins), you **MUST** use a **Docker Engine** >= 1.10.

## Container Deployment (Docker Container On Docker Hosts)

**In production**, a Dockerhost **MUST** only be used for **one** environment/system/customer combination. 

**Not permitted** are containers belonging to different 
- Dev/Prod 
- CustomerA/CustomerB 
- App1/App2

**Permitted** 
- DB-Container/Svc-Container/Log-Container of the **IDENTICAL** application.

