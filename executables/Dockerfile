ARG OPENMS_TAG=latest
FROM ghcr.io/openms/openms-library:${OPENMS_TAG} 

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests openjdk-17-jdk

WORKDIR /OpenMS
RUN mkdir /thirdparty && \
    git submodule update --init THIRDPARTY && \
    cp -r THIRDPARTY/All/* /thirdparty && \
    cp -r THIRDPARTY/Linux/64bit/* /thirdparty
ENV PATH="/thirdparty/LuciPHOr2:/thirdparty/MSGFPlus:/thirdparty/Sirius:/thirdparty/ThermoRawFileParser:/thirdparty/Comet:/thirdparty/Fido:/thirdparty/MaRaCluster:/thirdparty/Percolator:/thirdparty/SpectraST:/thirdparty/XTandem:/thirdparty/Sage:${PATH}"

WORKDIR /openms-build
RUN make -j3 TOPP && rm -rf src doc CMakeFiles 

WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"

# Metadata
LABEL base.image="ubuntu:22.04"
LABEL version="3.1"
LABEL software="OpenMS (tools)"
LABEL software.version="3.1.0-Ubuntu22.04"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
# to link to repo on github container registry
LABEL org.opencontainers.image.source https://github.com/OpenMS/OpenMS
