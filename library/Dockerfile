FROM openms/contrib

LABEL software="OpenMS lib"
LABEL software.version="develop"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /
RUN git clone --depth 1 https://github.com/OpenMS/OpenMS.git -b nightly
#RUN mkdir OpenMS
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DOPENMS_CONTRIB_LIBS="/contrib-build" -DCMAKE_PREFIX_PATH="/usr;/usr/local" -DBOOST_USE_STATIC=OFF -DWITH_GUI=OFF /OpenMS
RUN make OpenMS
