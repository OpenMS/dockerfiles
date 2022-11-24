# syntax=docker/dockerfile:1.3-labs
FROM ubuntu:18.04

# Step 1: set up a sane build system
USER root
	@@ -22,11 +22,11 @@ EOF

# Step 3: advanced dependencies
RUN apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev libglpk-dev libzip-dev zlib1g-dev libxerces-c-dev libbz2-dev libomp-dev libhdf5-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.62-dev \
                                                                     libboost-iostreams1.62-dev \
                                                                     libboost-regex1.62-dev \
                                                                     libboost-math1.62-dev \
                                                                     libboost-random1.62-dev
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
LABEL base.image="ubuntu:18.04"
LABEL version="3.0"
LABEL software="OpenMS (dependencies)"
LABEL software.version="2.7.0-Ubuntu18.04"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
# to link to repo on github container registry
LABEL org.opencontainers.image.source https://github.com/OpenMS/contrib

