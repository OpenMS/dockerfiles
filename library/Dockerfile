FROM openms/contrib

LABEL software="OpenMS library"
LABEL software.version="Release2.3.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /

RUN git clone --depth 1 --branch 'Release2.3.0'  --single-branch https://github.com/OpenMS/OpenMS.git

RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DOPENMS_CONTRIB_LIBS="/contrib-build" -DCMAKE_PREFIX_PATH="/usr;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DWITH_GUI=OFF -DBUILD_EXAMPLES=OFF -DBUILD_TESTING=OFF /OpenMS

RUN make OpenMS
