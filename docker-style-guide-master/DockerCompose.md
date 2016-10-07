# Docker Compose

The [documentation](https://docs.docker.com/compose/overview/) says, that

> Compose is a tool for defining and running multi-container Docker applications.

Because you can do a lot more that that, the **Style Guide** restrict some usages.

## Use docker-compose for orchestration only
You **MUST NOT** use **Docker Compose** for building **Docker Images**, but only for defining runtime environments.

This is BAD, because you create a NEW image/container on the **Docker Host**.

	  sp:
	    build: build/php:7-mysql
	    container_name: sp
	    volumes:
	    - "./src/sp:/var/www"

This is OK, because you use an existing image .

> Hint: The **Docker Image** registry.haufe.io/tsc/php:7-mysql does not really exist :-)

	  sp:
	    image: registry.haufe.io/tsc/php:7-mysql
	    container_name: sp
	    volumes:
	    - "./src/sp:/var/www"

> The exception to this rule is to an configuration/secret container that uses environment variables from the **Docker Compose** arguments OR from an `env_file`.

## NO secrets in **Docker Compose** definitions (or its repository)

Similar to the [NO secrets in Dockerfile](Dockerfile.md#no-secrets-in-dockerfile-or-its-repository), you **MUST NOT** store secrets in a Docker Compose definition (e.g. docker-compose.yml)

	$ cat docker-compose.yml
	  mysql:
	    image: mysql
	    container_name: mysql
	    volumes:
	    - "./data/mysql:/var/lib/mysql"
	    environment:
	    - "MYSQL_ROOT_PASSWORD=root"
	    - "MYSQL_DATABASE=saml"
	    - "MYSQL_USER=saml"
	    - "MYSQL_PASSWORD=saml"

The first improvement would be to use a file that is stored outside the **Dockerfile's** or **Docker Compose's** definition repository and only being retrieve or created at deployment time.

	$ cat docker-compose.yml
	  mysql:
	    image: mysql
	    container_name: mysql
	    volumes:
	    - "./data/mysql:/var/lib/mysql"
	$ cat .env
	MYSQL_ROOT_PASSWORD=root
	MYSQL_DATABASE=saml
	MYSQL_USER=saml
	MYSQL_PASSWORD=saml

With **Docker Compose** 0.6, you can use [variable expansion](https://docs.docker.com/compose/compose-file/#variable-substitution) so it is possible to do this.

	$ cat docker-compose.yml
	  mysql:
        image: mysql
        container_name: mysql
        volumes:
        - "./data/mysql:/var/lib/mysql"
        environment:
        - "MYSQL_ROOT_PASSWORD=$(ADMPWD)"
        - "MYSQL_DATABASE=$(DB)"
        - "MYSQL_USER=$(DBU)"
        - "MYSQL_PASSWORD=$(DBUPWD)"
	$ ADMPWD=root DB=saml DBU=saml DBUPWD=saml docker-compose up -d

This commandline can be created and executed by the deployment tools without anybody (human :-)) seeing the parameters as "plain text".