# Adapted from https://gist.github.com/nikos/eb27dce271f00cba2bb7
# and https://gist.github.com/rlouapre/39f3cf793f27895ae8d2
# Hat tips to Niko Schmuck <niko.auto@nava.de>
# and Richard Louapre <richard.louapre@marklogic.com>
# and MAINTAINER Norman Walsh <norman.walsh@marklogic.com>
###########################################
#
#  Usage:  
#    docker build  --build-arg java=<path to java sdk>  \
#                  -t tag  .
##################################################### 

FROM fedora:21
MAINTAINER David Lee <dlee@marklogic.com>

# Setup base system
RUN yum -y update; yum clean all
RUN yum -y install tar sudo applydeltarpm
RUN yum install -y openssh-server
RUN yum install -y libxml2 wget iputils iproute initscripts

WORKDIR /tmp
RUN wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm -O epel.rpm && \
  yum -y install epel.rpm && rm -f epel.rpm
  
# ./getjava.sh
ARG jdk
ADD ${jdk} /tmp/jdk.rpm
RUN yum -y install /tmp/jdk.rpm && rm -f /tmp/jdk.rpm 

ENV TERM rxvt-unicode
ENV JAVA_HOME /usr/java/latest

# Expose MarkLogic Server ports
EXPOSE 22 25 80 7997 7998 7999 8000 8001 8002 8002
ENTRYPOINT [ "/bin/bash" , "-c" ]