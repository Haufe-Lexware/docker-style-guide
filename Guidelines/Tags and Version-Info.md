# When creating an Docker image, ...

you can choose to leave it without a name and only use its id (a hash value).

But: Docker images are easier to use if you add a name and some versioning info, though.

An image name can be something quite short like

  myservice (a name meaningfull "only" on the "local" machine)
  
or a complete information where this image can be found in a registry (or being pushed to), 
what version it is and if it is a "special" release

myregistry/myuser/myservice:1.0.1-nginx

## Here is some help for what image names and versions should contain:

0. Image names should not contain version info "in themselves".  
  Example: There is no mysql4:1.0 or ubuntu14:0.4 but only mysql:4.x.x and ubuntu:14.0.4
  
1. container:latest - the most recent STABLE version (not necessarily the latest being build).  
  Meaning: The version everybody should use becasue he/she doesn't know any better.  
  Example: php or php:latest
  
2. container:major - this is for a specific version/featureset.  
  Meaning: For testing of forward- or backward compatibility  
  Example: php:4, php:5 or php:7  
  
3. container:major.minor - this is for a specific (compatible) version with a compatible featureset  
  Meaning: A (backward) container with no breaking changes, but new/removed plugins or optimizations  
  Example: mysql:5.6 vs mysql:5.7
  
4. container:major.minor.build - this is/must be EXACTLY THE current container. If anybody needs THIS container he has to use this tag.  
  Meaning: Builds are most likely security fixes etc. that are NOT intended to change any functionality.You might want to FORCE the presence of a specific (old) error, check the absence of a problem in a new container or guarnatee compatibility while using a new version  
  Example: mysql:5.6.28 vs mysql:5.7.10  
  
## Adding information to version

X.a. container:info  
X.b. container:major-info  
X.b. container:major.minor-info  
X.d. container:major.minor.build-info  
  Meaning: Most likely, there are "base" containers, that can be use in conjunction with other parts, but provide the same base service.  
  Example php:5.6.17-cli (is IDENTICAL to php:5.6.17 and so the default)  
  Example: php:5.6.17-apache is an php container installation that provides the apache webserver WITH php  
  Example: php:5.6.17-fpm is an php container that can be used with nginx (FPM=FastCGI Process Manager)
