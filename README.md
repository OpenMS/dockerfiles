# OpenMS Dockerfiles
This repository holds Dockerfiles for creating docker images for several OpenMS configurations based on different base images.
The configurations are found in self-descriptive folders for the Dockerfile:
 * batteries-included, a multistage build for the executables, including OpenMS' thirdparty binaries and JRE
 * contrib, basis for most images - for now only contains built libraries not available in base image OS repo
 * executables, base executables
 * library, the built OpenMS framework libraries (no GUI)
 * multistage, provides executables using docker build features introduced in 17.05, makes for slimmer images
 * pyOpenMS
 * travis

For now, they are completely unoptimized and mainly intended for internal use during continuous integration.
CI builds are triggered on DockerCloud whenever there is a push to contrib and whenever there is a push to our nightly branch (which is, as you could have guessed, at least once a night). 
Triggers and scheduled jobs are on our Jenkins.

Plan for when there is a release:
- create a new release branch release/v${VERSION}
- then first tag contrib, Thirdparty and OpenMS with Release${VERSION} on the appropriate branches/commits
- then change the git checkouts in the Dockerfiles to these tags
- check that they build
- tag the current head of the release/v${VERSION} branch with Release${VERSION} (e.g. Release2.2.0)

**Note**: docker-compose.yml holds the image names as used in the Dockerfiles. These should be kept as stable as possible, at some point they will reflect the names of the docker hub image names.
```bash
#{sudo} docker-compose create
#{sudo} docker-compose push
```
TODO build travis hooks around the YAML [https://docs.docker.com/docker-cloud/builds/advanced/#custom-build-phase-hooks]
