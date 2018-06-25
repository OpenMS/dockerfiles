FROM openms/library 

LABEL software="OpenMS executables"
LABEL software.version="Release2.3.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /openms-build

RUN make TOPP && make UTILS

WORKDIR /

ENV PATH /openms-build/bin/:${PATH}

ENV LD_LIBRARY_PATH /openms-build/lib/:${LD_LIBRARY_PATH}

ENV OPENMS_DATA_PATH /OpenMS/share/OpenMS

RUN useradd -u 1001 -U -d /home/OpenMSuser -m -s /bin/bash OpenMSuser

USER OpenMSuser

ENV HOME /home/OpenMSuser

WORKDIR /home/OpenMSuser