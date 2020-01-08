FROM openms/contrib:latest

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd /OpenMS && rm -rf .git share/OpenMS/examples/

RUN mkdir openms-build
WORKDIR /openms-build

# Load the Qt5 environment and configure
RUN /bin/bash -c "QT_ENV=$(find /opt -name 'qt*-env.sh') && source ${QT_ENV} && cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS
