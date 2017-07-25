FROM openms/library

WORKDIR /openms-build

RUN apt-get update -y && apt-get install -y python-pip python-dev python-numpy
RUN pip install nose
RUN pip install -U setuptools
RUN pip install Cython==0.25.2
RUN pip install autowrap==0.11.0
RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DPYOPENMS=On ../OpenMS

# make OpenMS library
RUN make pyopenms

# install
WORKDIR /openms-build/pyOpenMS
RUN python setup.py install
WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"
