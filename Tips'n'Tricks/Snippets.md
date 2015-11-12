This will be the place for really small (and even dirty) tricks that can help you (on your LOCAL) machine.
Most of those you wouldn't dare to introduce into a development, test/staging or production environment, but it might help YOU on your local machine getting things done.

## Building Docker-Images using directory names

    docker build --tag `pwd|xargs basename` .

Note: The command has to be executed inside the directory that contains the Dockerfile.

---

[Tips'n'Tricks](Tips'n'Tricks)  
[Docker Docs - Home](../wiki/Home)  
