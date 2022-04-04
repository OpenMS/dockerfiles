# OpenMS Dockerfiles
This repository holds Dockerfiles for creating docker images for several OpenMS configurations based on different base images.
For now, they are completely unoptimized and mainly intended for internal use during continuous integration.
For the most important images (contrib, manylinux2014, executables) builds are triggered with GitHub Actions and published
on https://github.com/orgs/OpenMS/packages.

# Writing dockerfiles
See e.g. https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
By now, we require docker buildx to build them to include newer features https://docs.docker.com/buildx/working-with-buildx/

TODO Use dockercompose YAML scripts to correctly resolve dependencies and reduce image size by not adding tools that are no dependencies.
https://docs.docker.com/docker-cloud/builds/advanced/#custom-build-phase-hooks
