# docker build -t snowsprout/elasticsearch-eunjeon .
# Basically installed ElasticSearch


FROM elasticsearch:5.4

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*

#Install mecab-ko
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

#Install mecab-ko-dic
RUN \
  cd /opt &&\
  wget https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/mecab-ko-dic-1.6.1-20140814.tar.gz &&\
  tar xvf mecab-ko-dic-1.6.1-20140814.tar.gz &&\
  cd /opt/mecab-ko-dic-1.6.1-20140814 &&\
  ./autogen.sh &&\
  ./configure &&\
  make &&\
  make install

ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8

RUN \
  cd /opt &&\
  wget https://mecab.googlecode.com/files/mecab-java-0.996.tar.gz &&\
  tar xvf mecab-java-0.996.tar.gz &&\
  cd /opt/mecab-java-0.996 &&\
  sed -i 's|/usr/lib/jvm/java-6-openjdk/include|/usr/lib/jvm/java-8-oracle/include|' Makefile &&\
  make &&\
  cp libMeCab.so /usr/local/lib

# Define mountable directories.
VOLUME ["/data"]

# Mount elasticsearch.yml config
ADD config/elasticsearch.yml /elasticsearch/config/elasticsearch.yml

RUN /elasticsearch/bin/plugin --install analysis-mecab-ko-0.17.0 --url https://bitbucket.org/eunjeon/mecab-ko-lucene-analyzer/downloads/elasticsearch-analysis-mecab-ko-0.17.0.zip

# Define working directory.
WORKDIR /data

# Define default command.
CMD /elasticsearch/bin/elasticsearch -Djava.library.path=/usr/local/lib

# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300