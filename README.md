# OpenMS Dockerfiles
This repository holds Dockerfiles for creating docker images for several OpenMS configurations based on different base images.
For now they are completely unoptimized and mainly intended for internal use during continuous integration.
For now, builds are triggered on DockerCloud whenever there is a push to contrib and whenever there is a push to our nightly branch (which 
is, as you could have guessed, at least once a night). Triggers and scheduled jobs are on our Jenkins.

Plan for when there is a release:
- create a new release branch release/v${VERSION}
- then first tag contrib, Thirdparty and OpenMS with Release${VERSION} on the appropriate branches/commits
- then change the git checkouts in the Dockerfiles to these tags
- check that they build
- tag the current head of the release/v${VERSION} branch with Release${VERSION} (e.g. Release2.2.0)
