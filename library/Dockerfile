FROM openms/contrib:latest

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd /OpenMS && rm -rf .git share/OpenMS/examples/

RUN mkdir openms-build
WORKDIR /openms-build

# configure
RUN /bin/bash -c "cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS
