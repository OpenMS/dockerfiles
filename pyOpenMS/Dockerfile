FROM openms/library

LABEL software="pyOpenMS"
LABEL software.version="Release2.3.0"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:16.04"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /openms-build

RUN apt-get update -y 
RUN apt-get install -y python-pip \
				python-dev \
				python-numpy
RUN pip install nose
RUN pip install -U setuptools
RUN pip install Cython
RUN pip install autowrap
RUN cmake  -DOPENMS_CONTRIB_LIBS="/contrib-build" -DCMAKE_PREFIX_PATH="/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DWITH_GUI=OFF -DBUILD_EXAMPLES=OFF -DBUILD_TESTING=OFF -DPYOPENMS=On /OpenMS

RUN make pyopenms

WORKDIR /openms-build/pyOpenMS

RUN python setup.py install

WORKDIR /

ENV PATH /openms-build/bin/:${PATH}

WORKDIR /
ENV PATH /OpenMS/bin/:${PATH}
ENV LD_LIBRARY_PATH /OpenMS/lib/:${LD_LIBRARY_PATH}
ENV OPENMS_DATA_PATH /OpenMS/share/OpenMS

RUN useradd -u 1001 -U -d /home/OpenMSuser -m -s /bin/bash OpenMSuser
USER OpenMSuser
ENV HOME /home/OpenMSuser
WORKDIR /home/OpenMSuser