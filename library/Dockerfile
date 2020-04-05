ARG OPENMS_TAG=latest
FROM openms/contrib:${OPENMS_TAG}
ARG OPENMS_BRANCH=develop

WORKDIR /
# branch will be develop for the Dockerfiles on master
RUN git clone -b ${OPENMS_BRANCH} --single-branch https://github.com/OpenMS/OpenMS.git && cd /OpenMS

RUN mkdir openms-build
WORKDIR /openms-build

# configure
RUN /bin/bash -c "cmake -DCMAKE_BUILD_TYPE='Release' -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF ../OpenMS"

# make OpenMS library
RUN make OpenMS
