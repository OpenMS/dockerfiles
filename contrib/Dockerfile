FROM ubuntu:14.04

LABEL software="OpenMS contrib"
LABEL software.version="develop"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/contrib/master/License.txt"
LABEL base.image="ubuntu:14.04"

ENV DEBIAN_FRONTEND noninteractive

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

# Step 4: install Qt4
RUN apt-get install -y --no-install-recommends --no-install-suggests qt4-dev-tools qt4-default qt4-qtconfig qt4-qmake
RUN apt-get install -y --no-install-recommends --no-install-suggests libqt4-dev libqt4-opengl-dev libqt4-svg libqtwebkit-dev

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

