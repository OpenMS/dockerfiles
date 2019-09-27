FROM ubuntu:14.04

# Step 1: set up a sane build system
USER root

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf automake patch libtool make git
RUN apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties

# Step 2: get an up-to date cmake 3.x for ubuntu 14.04
RUN add-apt-repository ppa:george-edison55/cmake-3.x
RUN apt-get -y update
RUN apt-get install -y cmake

# Step 3: advanced dependencies
RUN apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev libglpk-dev libzip-dev zlib1g-dev libxerces-c-dev libbz2-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.54-dev \
                                                                     libboost-iostreams1.54-dev \
                                                                     libboost-regex1.54-dev \
                                                                     libboost-math1.54-dev \
                                                                     libboost-random1.54-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libhdf5-dev

# Step 4: Qt5
RUN add-apt-repository ppa:beineri/opt-qt571-trusty 
RUN apt-get -y update
RUN apt-get install -y qt57base qt57webengine qt57svg libgl1-mesa-dev && rm -rf /opt/qt57/examples

###################################
# Step 5: Compiled dependencies
RUN git clone https://github.com/OpenMS/contrib.git && rm -rf contrib/.git/
RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=SEQAN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=WILDMAGIC ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=EIGEN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=COINOR ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=SQLITE ../contrib && rm -rf archives src

WORKDIR /

# Metadata
LABEL base.image="openms/contrib"
LABEL version="3.0"
LABEL software="OpenMS (dependencies)"
LABEL software.version="openms-contrib-v2.5.1"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

