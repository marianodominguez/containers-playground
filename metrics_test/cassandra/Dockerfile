FROM centos:7

RUN groupadd -g 502 marun
RUN useradd -u 502 -g 502 -d /home/marun marun

WORKDIR /home/marun

ENV version=3.11.1
ENV BUILD_VERSION=b11
ENV JAVA_VERSION=8u172
ENV JAVA_HOME=/usr/java/latest

RUN yum -y install wget

RUN wget -SL --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
 "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/a58eab1ec242421181065cdc37240b08/jdk-$JAVA_VERSION-linux-x64.rpm" \
 -O /tmp/jdk-8-linux-x64.rpm

RUN yum -y install /tmp/jdk-8-linux-x64.rpm

RUN alternatives --install /usr/bin/java jar /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 2000

USER marun

RUN wget -SL -O apache-cassandra-${version}-bin.tar.gz \
http://mirrors.advancedhosters.com/apache/cassandra/${version}/apache-cassandra-${version}-bin.tar.gz

RUN tar -xzf apache-cassandra-${version}-bin.tar.gz \
  && mv apache-cassandra-${version} apache-cassandra \
  && rm  apache-cassandra-${version}-bin.tar.gz

CMD ["/home/marun/apache-cassandra/bin/cassandra", "-f" ]
