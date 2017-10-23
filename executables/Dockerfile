FROM openms/library 

LABEL software="OpenMS executables"
LABEL software.version="develop"
LABEL website="https://www.OpenMS.de"
LABEL documentation="https://www.OpenMS.de/documentation/"
LABEL tags="proteomics, mass spectrometry"
LABEL license="https://raw.githubusercontent.com/OpenMS/OpenMS/develop/License.txt"
LABEL base.image="ubuntu:14.04"

WORKDIR /openms-build

RUN make TOPP && make UTILS && rm -rf src doc CMakeFiles 

WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"

