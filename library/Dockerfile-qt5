FROM openms/contrib:qt5-v2.0

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd /OpenMS && git checkout feature/qt5 && rm -rf .git share/OpenMS/examples/

RUN mkdir openms-build
WORKDIR /openms-build

# Load the Qt5 environment and configure
RUN QT_ENV=$(find /opt -name 'qt*-env.sh') && /bin/bash -c "source ${QT_ENV} && cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS -j6

