# docker build -t snowsprout/elasticsearch .

FROM elasticsearch

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN apt-get update
RUN apt-get install zip

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
  cd /opt/mecab-ko-dic-2.0.1-20150920.tar.gz &&\
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
  sed -i 's|/usr/lib/jvm/java-6-openjdk/include|/usr/lib/jvm/java-8-oracle/include|' Makefile &&\
  make &&\
  cp libMeCab.so /usr/local/lib

ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8


RUN \
	cd /usr/share/elasticsearch &&\
	bash <(curl -s https://bitbucket.org/eunjeon/seunjeon/raw/master/elasticsearch/scripts/downloader.sh) -e 5.5.0 -p 2.4.0.1 &&\
	./bin/elasticsearch-plugin install file://`pwd`/elasticsearch-analysis-seunjeon-2.4.0.1.zip &&\