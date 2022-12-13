# syntax=docker/dockerfile:1.3-labs
FROM ubuntu:22.04

# Step 1: set up a sane build system
USER root

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf automake patch libtool make git gpg wget ca-certificates curl
RUN update-ca-certificates

# Step 2: get an up-to date cmake (HEREDOC needs DOCKER_BUILDKIT=1 enabled or build with "docker buildx")
RUN <<-EOF
    cmake_ubuntu_version=$(lsb_release -cs)
    if ! wget -q --method=HEAD "https://apt.kitware.com/ubuntu/dists/$cmake_ubuntu_version/Release"; then
      bash -c "$(wget -O - https://apt.kitware.com/kitware-archive.sh)"
    else
      wget -qO - https://apt.kitware.com/kitware-archive.sh | bash -s -- --release $cmake_ubuntu_version
    fi
    apt-get -y update
    apt-get install -y cmake
EOF

# Step 3: advanced dependencies
RUN apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev libglpk-dev libzip-dev zlib1g-dev libxerces-c-dev libbz2-dev libomp-dev libhdf5-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.74-dev \
                                                                     libboost-iostreams1.74-dev \
                                                                     libboost-regex1.74-dev \
                                                                     libboost-math1.74-dev \
                                                                     libboost-random1.74-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests qtbase5-dev libqt5svg5-dev libqt5opengl5-dev

###################################
# Step 4: Compiled dependencies
RUN git clone https://github.com/OpenMS/contrib.git && rm -rf contrib/.git/
RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=EIGEN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=COINOR ../contrib && rm -rf archives src

WORKDIR /

# Metadata
LABEL base.image="ubuntu:22.04"
LABEL version="3.0"
LABEL software="OpenMS (dependencies)"
LABEL software.version="3.0.0-Ubuntu22.04"
LABEL description="Baseimage to build OpenMS: C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
# to link to repo on github container registry
LABEL org.opencontainers.image.source https://github.com/OpenMS/contrib
