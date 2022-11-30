FROM openms/library

WORKDIR /openms-build

RUN apt-get update -y && apt-get install -y python-pip python-dev python-numpy
RUN pip install pytest
RUN pip install -U setuptools
RUN pip install Cython
RUN pip install autowrap
RUN pip install pandas
RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DPYOPENMS=On ../OpenMS

# make OpenMS library
RUN make pyopenms

# install
WORKDIR /openms-build/pyOpenMS
RUN pip install dist/*.whl
WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"

# Metadata
LABEL base.image="ubuntu:22.04"
LABEL version="3.0"
LABEL software="OpenMS (library+tools+pyopenms)"
LABEL software.version="3.0.0-Ubuntu22.04"
LABEL description="C++ libraries and tools for MS/MS data analysis with python bindings"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"
