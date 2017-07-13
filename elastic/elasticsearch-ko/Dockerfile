# docker build -t snowsprout/elasticsearch-ko .

FROM elasticsearch:5.5.0

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN \
	apt-get update &&\
	apt-get install -y build-essential &&\
	apt-get install -y zip automake openjdk-8-jdk

#install mecab-ko
RUN \
  cd /opt &&\
  wget https://bitbucket.org/eunjeon/mecab-ko/downloads/mecab-0.996-ko-0.9.2.tar.gz &&\
  tar xvf mecab-0.996-ko-0.9.2.tar.gz &&\
  cd /opt/mecab-0.996-ko-0.9.2 &&\
  ./configure &&\
  make &&\
  make check &&\
  make install &&\
  ldconfig

#install mecab-ko-dic
RUN \
  cd /opt &&\
  wget https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/mecab-ko-dic-2.0.1-20150920.tar.gz &&\
  tar xvf mecab-ko-dic-2.0.1-20150920.tar.gz &&\
  cd /opt/mecab-ko-dic-2.0.1-20150920 &&\
  ./autogen.sh &&\
  ./configure &&\
  make &&\
  make install

#install mocab-java
RUN \
  cd /opt &&\
  wget https://bitbucket.org/eunjeon/mecab-java/downloads/mecab-java-0.996.tar.gz &&\
  tar xvf mecab-java-0.996.tar.gz &&\
  cd /opt/mecab-java-0.996 &&\
  sed -i 's|/home/parallels/Programs/jdk1.7.0_75/include|/usr/lib/jvm/java-8-openjdk-amd64/include|' Makefile &&\
  sed -i 's|$(CXX) -O3|$(CXX) -O1|' Makefile &&\  
  make &&\
  cp libMeCab.so /usr/local/lib

ENV ES_JAVA_OPTS "-Dfile.encoding=UTF8 -Djava.library.path=/usr/local/lib -Des.security.manager.enabled=false"
#ENV ES_JAVA_OPTS "$ES_JAVA_OPTS "

RUN cd /usr/share/elasticsearch
RUN ["/bin/bash", "-c", "bash <(curl -s https://bitbucket.org/eunjeon/seunjeon/raw/master/elasticsearch/scripts/downloader.sh) -e 5.5.0 -p 2.4.0.1"]
#RUN cd /usr/share/elasticsearch &&\
#	./bin/elasticsearch-plugin install file://`pwd`/elasticsearch-analysis-seunjeon-2.4.0.1.zip



# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300	