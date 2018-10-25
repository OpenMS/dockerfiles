FROM openms/contrib

LABEL software="OpenMS library"
LABEL software.version="LFQtool2.4.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /

RUN git clone --depth 1 --branch 'feature/proteomic_lfq'  --single-branch https://github.com/mwalzer/OpenMS.git

RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DOPENMS_CONTRIB_LIBS="/contrib-build" -DCMAKE_PREFIX_PATH="/usr;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DWITH_GUI=OFF -DBUILD_EXAMPLES=OFF -DBUILD_TESTING=OFF /OpenMS

RUN make OpenMS
