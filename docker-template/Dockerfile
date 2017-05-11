FROM ubuntu:16.04
RUN apt-get update
RUN apt-get -y install apt-transport-https wget
RUN wget -qO - https://z.cash/gpg-pubkeys/zcash.asc | apt-key add -
RUN echo "deb https://apt.z.cash jessie main" | tee /etc/apt/sources.list.d/zcash.list
RUN apt-get update
RUN apt-get -y install zcash
RUN zcash-fetch-params
RUN cd /root/; mkdir .zcash; cd .zcash/; touch zcash.conf
RUN echo "rpcuser=$USERNAME" >> /root/.zcash/zcash.conf
RUN echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >> /root/.zcash/zcash.conf
RUN echo "gen=1" >> /root/.zcash/zcash.conf

