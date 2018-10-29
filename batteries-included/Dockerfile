FROM openms/library as library
ENV DEBIAN_FRONTEND noninteractive

WORKDIR /openms-build

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests binutils subversion

RUN make TOPP && make UTILS  

RUN for l in lib/*.so; do strip --strip-all $l; done

RUN mkdir /opt/thirdparty && \
    svn checkout https://github.com/OpenMS/THIRDPARTY/trunk/Linux/64bit /opt/thirdparty && \
    rm -rf /opt/thirdparty/.svn && \
    svn checkout https://github.com/OpenMS/THIRDPARTY/trunk/All /opt/thirdparty && \
    rm -rf /opt/thirdparty/.svn

ENV PATH /opt/thirdparty/Fido:/opt/thirdparty/LuciPHOr2:/opt/thirdparty/MSGFPlus:/opt/thirdparty/MyriMatch:/opt/thirdparty/OMSSA:/opt/thirdparty/XTandem:/opt/thirdparty/Comet:/opt/thirdparty/SpectraST:/opt/thirdparty/Sirius:/opt/thirdparty/Percolator:/opt/thirdparty/MaRaCluster:/opt/thirdparty/crux:${PATH}



FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive

LABEL software="OpenMS batteries included"
LABEL software.version="LFQtool2.4.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

RUN mkdir /OpenMS
WORKDIR /OpenMS

COPY --from=library /OpenMS/AUTHORS .
COPY --from=library /OpenMS/CHANGELOG .
COPY --from=library /OpenMS/LICENSE .
COPY --from=library /OpenMS/README .
COPY --from=library /OpenMS/share/OpenMS/CHEMISTRY /OpenMS/share/OpenMS/CHEMISTRY
COPY --from=library /OpenMS/share/OpenMS/CV /OpenMS/share/OpenMS/CV
COPY --from=library /OpenMS/share/OpenMS/MAPPING /OpenMS/share/OpenMS/MAPPING
COPY --from=library /OpenMS/share/OpenMS/SCHEMAS /OpenMS/share/OpenMS/SCHEMAS
COPY --from=library /OpenMS/share/OpenMS/XSL /OpenMS/share/OpenMS/XSL
COPY --from=library /OpenMS/share/OpenMS/SCRIPTS /OpenMS/share/OpenMS/SCRIPTS

COPY --from=library /openms-build/bin /OpenMS/bin
COPY --from=library /openms-build/lib /OpenMS/lib

COPY --from=library /opt/thirdparty /opt/thirdparty

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev \
													python-software-properties \
													qtbase5-dev \
													libqt5svg5-dev \
													libzip-dev \
													libglpk-dev \
													zlib1g-dev \
													libxerces-c-dev \
													seqan-dev \
													libbz2-dev \
													coinor-libcoinmp-dev
# install R 3.5
RUN apt-get install -y software-properties-common apt-transport-https
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
RUN add-apt-repository 'deb [arch=amd64,i386] https://cloud.r-project.org/bin/linux/ubuntu xenial-cran35/'
RUN apt-get update
RUN apt install -y r-base
# install MSstats
RUN Rscript -e 'source("https://bioconductor.org/biocLite.R"); biocLite("MSstats",ask=FALSE,suppressUpdates=TRUE);'

RUN apt-get install -y --no-install-recommends --no-install-suggests default-jre				      
RUN apt-get autoremove -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/lib/{cache,log}

#example input for kicking tires
#COPY --from=library /OpenMS/share/OpenMS/examples /OpenMS/share/OpenMS/examples

WORKDIR /
ENV PATH /OpenMS/bin/:${PATH}
ENV LD_LIBRARY_PATH /OpenMS/lib/:${LD_LIBRARY_PATH}
ENV PATH /opt/thirdparty/Fido:/opt/thirdparty/LuciPHOr2:/opt/thirdparty/MSGFPlus:/opt/thirdparty/MyriMatch:/opt/thirdparty/OMSSA:/opt/thirdparty/XTandem:/opt/thirdparty/Comet:/opt/thirdparty/SpectraST:/opt/thirdparty/Sirius:/opt/thirdparty/Percolator:/opt/thirdparty/MaRaCluster:/opt/thirdparty/crux:${PATH}
ENV OPENMS_DATA_PATH /OpenMS/share/OpenMS

RUN useradd -u 1001 -U -d /home/OpenMSuser -m -s /bin/bash OpenMSuser
USER OpenMSuser
ENV HOME /home/OpenMSuser
WORKDIR /home/OpenMSuser
