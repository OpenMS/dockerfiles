FROM ubuntu:16.04

LABEL software="OpenMS contrib packages"
LABEL software.version="LFQtool2.4.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/contrib/master/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive

USER root

RUN apt-get -y update

RUN apt-get install -y --no-install-recommends --no-install-suggests ca-certificates \
													git \
													build-essential \
													cmake \
													autoconf \
													patch \
													libtool \
													automake \
													libgomp1 \
													python-software-properties \
													qtbase5-dev \
													libqt5svg5-dev \
													libsvm-dev\
													libglpk-dev \
													zlib1g-dev \
													libxerces-c-dev \
													seqan-dev \
													libbz2-dev \
													coinor-libcoinmp-dev

RUN git clone --depth 1 --branch 'master'  --single-branch https://github.com/OpenMS/contrib.git

RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=ALL ../contrib && rm -rf archives src

WORKDIR /

