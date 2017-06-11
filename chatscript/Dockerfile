# docker build -t snowsprout/chatscript .

FROM ubuntu:trusty

# Install Packages
RUN apt-get update
RUN apt-get install -y --force-yes autoconf \
curl \
git \
wget \
unzip

RUN set -ex \
	&& mkdir -p /usr/local/apps \
	&& cd /usr/local/apps \
	&& wget https://github.com/bwilcox-1234/ChatScript/archive/master.zip \
    && unzip master.zip \
    && mv ./ChatScript-master ./chatScript \
    && chmod 755 ./chatScript/BINARIES/LinuxChatScript64

RUN ln -s /usr/local/apps/chatScript/BINARIES/LinuxChatScript64 /bin/chatscript
RUN chmod +x /bin/chatscript

ENV PORT 1024
ENV DEBIAN_FRONTEND noninteractive

#Port Expose
EXPOSE 1024

# Startup
USER root

CMD ["chatscript"]