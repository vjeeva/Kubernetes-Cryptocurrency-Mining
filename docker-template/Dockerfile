FROM ubuntu:16.04
RUN apt-get -y update
RUN apt-get -y install software-properties-common
RUN add-apt-repository -y ppa:ethereum/ethereum
RUN apt-get -y update
RUN apt-get -y install ethminer
EXPOSE 80
CMD ethminer -C -F <farm-url-here>
