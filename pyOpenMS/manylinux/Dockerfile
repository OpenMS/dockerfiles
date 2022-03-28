## openms/manylinux is based on hroest/manylinux2014_qt59:v1.1
FROM quay.io/pypa/manylinux2014_x86_64

ARG OPENMS_BRANCH="develop"
ARG OPENMS_VERSION="latest"

# Override yum to work around the problem with newly built libcurl.so.4
# https://access.redhat.com/solutions/641093
RUN echo $'#!/bin/bash\n\
LD_PRELOAD=/usr/lib64/libcurl.so.4 /usr/bin/yum "$@"' > /usr/local/bin/yum && chmod a+x /usr/local/bin/yum

RUN yum install -y wget
RUN yum install -y xz qt5-qtbase-devel 
RUN yum install -y qt5-qtbase-devel qt5-qtsvg qt5-qtsvg-devel python-devel 
# RUN yum install -y libsvm-devel glpk-devel libzip-devel zlib-devel xerces-c-devel bzip2-devel sqlite-devel hdf5-devel
RUN yum install -y libtool

RUN yum install -y cmake3
RUN ln -s /usr/bin/cmake3 /usr/bin/cmake

# install contrib based on the OpenMS branch used! 
RUN git clone https://github.com/OpenMS/OpenMS.git --branch "$OPENMS_BRANCH" --single-branch && \
    cd OpenMS && \
    git submodule update --init contrib && \
    mkdir contrib-build && \
    cd contrib-build && \
    cmake -DBUILD_TYPE=ALL ../contrib && \
    rm -rf archives src && \
    cp -r . /contrib-build &&\
    cd / && \
    rm -rf OpenMS

WORKDIR /

# Metadata
LABEL base.image="manylinux2014_x86_64"
LABEL version="1.0"
LABEL software="OpenMS (dependencies for manylinux2010)"
LABEL software.version="$OPENMS_VERSION"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
