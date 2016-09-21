FROM base/ubuntu14.04

MAINTAINER Kwangmyung Kim <kwangmyung.kim@gmail.com>

# Install JDK 8u102
RUN wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u102-b14/jdk-8u102-linux-x64.tar.gz &&\
mkdir /opt/jdk && tar -zxf jdk-8u102-linux-x64.tar.gz -C /opt/jdk \
&& rm /jdk-8u102-linux-x64.tar.gz

WORKDIR /opt

RUN update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_102/bin/java 100

RUN update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_102/bin/javac 100

WORKDIR /root

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /opt/jdk/jdk1.8.0_102
