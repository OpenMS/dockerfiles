ARG OPENMS_TAG=latest
FROM ghcr.io/openms/contrib:${OPENMS_TAG}
ARG OPENMS_BRANCH=develop

WORKDIR /
# branch will be develop for the Dockerfiles on master
RUN git clone -b ${OPENMS_BRANCH} --single-branch https://github.com/OpenMS/OpenMS.git && cd /OpenMS

RUN mkdir openms-build
WORKDIR /openms-build

# configure
RUN /bin/bash -c "cmake -DCMAKE_BUILD_TYPE='Release' -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS

# Metadata
LABEL base.image="ubuntu:22.04"
LABEL version="3.0"
LABEL software="OpenMS (library)"
LABEL software.version="3.2.0-Ubuntu22.04"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
# to link to repo on github container registry
LABEL org.opencontainers.image.source https://github.com/OpenMS/OpenMS
