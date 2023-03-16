# Docker Registry Facade [![Build Status](https://github.com/httptoolkit/docker-registry-facade/workflows/CI/badge.svg)](https://github.com/httptoolkit/docker-registry-facade/actions) [![Pull from Docker Hub](https://img.shields.io/badge/Pull%20from-Docker%20Hub-0db7ed)](https://hub.docker.com/r/pimterry/docker-registry-facade) [![Pull from GitHub Container Registry](https://img.shields.io/badge/Pull%20from-GHCR-%23333)](https://ghcr.io/httptoolkit/docker-registry-facade)

> _Part of [HTTP Toolkit](https://httptoolkit.com): powerful tools for building, testing & debugging HTTP(S)_

A tiny self-hostable Docker Registry facade - own your registry URL without running your own registry.

This is intended to help organizations publishing images mitigate the upcoming Dockerpocalypse by:

* Allowing immediate migration to a self-controlled registry URL now, while still using Docker Hub as the backend temporarily.
* Ensuring that organizations control their own image URLs, so they can migrate registries in future without risking the same issues.

## How to run this

To test this out locally, try this:

```
docker run \
    -e'REGISTRY_HOST=registry.hub.docker.com' \
    -p443:443 \
    ghcr.io/httptoolkit/docker-registry-facade
```

and then pull from it, e.g. with:

```
docker pull localhost/pimterry/docker-registry-facade
```

To configure this further, you can set the following environment variables:

* `REGISTRY_HOST` (required): the hostname of the target registry, e.g. `registry.hub.docker.com`
* `REGISTRY_ORG`: the org on the target registry which should be supported. If specified, only images from this organization will be accessible. If not, this facade will be usable to pull all images from any organization.
* `CACHE_TIMEOUT`: the redirects that this image serves come with cache headers to try & limit unnecessary requests. The default timeout is 1 day, but you can reduce it by specifying a number of seconds here.