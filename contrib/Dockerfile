FROM ubuntu:16.04

LABEL software="OpenMS contrib packages"
LABEL software.version="Release2.3.0"
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
													libqt4-dev \
													libqtwebkit-dev \
													libqt4-opengl-dev \
													libgomp1 \
													python-software-properties

RUN git clone --depth 1 --branch 'Release2.3.0'  --single-branch https://github.com/OpenMS/contrib.git

RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=ALL ../contrib && rm -rf archives src

WORKDIR /

