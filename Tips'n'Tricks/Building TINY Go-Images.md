Using the docker image centurylink/golang-builder ( https://github.com/CenturyLinkLabs/golang-builder ), 
it is possible to create "Single statically linked Go-Application" docker images. 

You have to follow some rules (see webpage) but it's worth the effort.

    docker run --rm -v "$(pwd):/src" -v /var/run/docker.sock:/var/run/docker.sock \
      centurylink/golang-builder dockerhub.haufe-lexware.com/dockerui

---

