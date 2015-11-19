# How to write your own Dockerfile

> There are many helpful online resources about writing Dockerfiles
> One of the best starting points is the corresponding Docker documentation
Michael Crosby has provided a good list of best practises  [PART 1][1] [PART 2][2]

# Use the cache, Luke ... (whoever misses the joke, this is a "quote" from STAR WARS)
During Dockerfile development, keep RUN commands separate, so you can easily add new commands and are still being cached
Starting point. The following (single example line) is cached by Docker.

    RUN cpanm XML::Sample

Following the best-practices, the following reduces the number of images but forces the build process to "redo" the first (already cached) command.

Basically, you modified the previous command to a longer command line that is UNCACHED.

    RUN cpanm XML::Sample \
        cpanm HTML::Sample


Keeping this example simple, this version leaves the cached first line untouched and adds a new command. For the first one, the cache is being used and only the second one is REALLY PROCESSED (and cached afterwards (smile)).

    RUN cpanm XML::Sample
    RUN cpanm HTML::Sample

Put package commands like yum update, apt-get update etc. BEFORE commands like ADD and COPY. If added/copied files are changed, they might trigger a new package command.

# TBC ...

[1]: http://crosbymichael.com/dockerfile-best-practices.html
[2]: http://crosbymichael.com/dockerfile-best-practices-take-2.html

---

