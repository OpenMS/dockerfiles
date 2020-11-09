FROM quay.io/pypa/manylinux2014_x86_64

RUN yum install -y wget
RUN yum install -y xz qt5-qtbase-devel 
# RUN yum install -y boost-regex boost-chrono boost-date-time boost-filesystem boost-iostreams boost-math
# RUN yum install -y boost-python boost-serialization boost-system boost-thread 
RUN yum install -y qt5-qtbase-devel qt5-qtsvg qt5-qtsvg-devel python-devel 
RUN yum install -y libsvm-devel glpk-devel libzip-devel zlib-devel xerces-c-devel bzip2-devel sqlite-devel hdf5-devel
RUN yum install -y libtool

## this is hroest/manylinux2014_qt59:v1
RUN yum install -y cmake3
RUN ln -s /usr/bin/cmake3 /usr/bin/cmake

## this is hroest/manylinux2014_qt59:v1.1

# install contrib (need ALL here to build static libs)
RUN git clone https://github.com/OpenMS/contrib.git && \
    mkdir contrib-build && \
    cd /contrib-build && \
    cmake -DBUILD_TYPE=ALL ../contrib && \
    rm -rf archives src && \
    cd / && \
    rm -rf contrib

##     cmake -DBUILD_TYPE=SEQAN ../contrib && \
##     cmake -DBUILD_TYPE=COINOR ../contrib && \
##     cmake -DBUILD_TYPE=EIGEN ../contrib && \
##     cmake -DBUILD_TYPE=WILDMAGIC ../contrib && \
## 

WORKDIR /

## this is hroest/manylinux2014_qt59_contrib:v1.1


# Metadata
LABEL base.image="manylinux2014_x86_64"
LABEL version="2.0"
LABEL software="OpenMS (dependencies for manylinux2010)"
LABEL software.version="qt5-v2.5.1"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

