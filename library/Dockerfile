ARG OPENMS_TAG
FROM openms/contrib:latest

WORKDIR /
RUN git clone -b develop --single-branch https://github.com/OpenMS/OpenMS.git && cd /OpenMS

RUN mkdir openms-build
WORKDIR /openms-build

# configure
RUN /bin/bash -c "cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS
