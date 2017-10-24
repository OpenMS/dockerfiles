FROM openms/library as library
ENV DEBIAN_FRONTEND noninteractive

WORKDIR /openms-build

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests binutils

RUN for l in lib/*.so; do strip --strip-all $l; done
#RUN strip --strip-all lib/libOpenSwathAlgo.so
#RUN strip --strip-all lib/libSuperHirn.so

RUN make TOPP && make UTILS && rm -rf src doc CMakeFiles 

FROM ubuntu:14.04
ENV DEBIAN_FRONTEND noninteractive

LABEL software="OpenMS executables"
LABEL software.version="develop"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:14.04"

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
COPY --from=library /openms-build/bin .
COPY --from=library /openms-build/lib .

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev \
								libglpk-dev \ 
								libzip-dev \
                                                                zlib1g-dev \
								libxerces-c-dev \
								libbz2-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.54-dev \
                                                                     libboost-iostreams1.54-dev \
                                                                     libboost-regex1.54-dev \
                                                                     libboost-math1.54-dev \
                                                                     libboost-random1.54-dev
RUN apt-get install -y --no-install-recommends --no-install-suggests libqt4-dev \
								libqt4-opengl-dev \
								libqt4-svg \
								libqtwebkit-dev


WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"

