FROM aeonproject/base
MAINTAINER 'Aeon Builds <builds+dockerfile@aeon.io>'

ENV GLIBC_VERSION 2.22-r8
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 65
ENV JAVA_VERSION_BUILD 17
ENV JAVA_PACKAGE       server-jre

RUN apk update \
 && curl -Ls https://github.com/andyshinn/alpine-pkg-glibc/releases/download/2.22-r8/glibc-${GLIBC_VERSION}.apk > /tmp/glibc-${GLIBC_VERSION}.apk \
 && apk add --allow-untrusted /tmp/glibc-${GLIBC_VERSION}.apk \
 && rm /tmp/*

RUN mkdir /opt && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie"\
  http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \
    | tar -xzf - -C /opt &&\
    ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/java &&\
    rm -rf /opt/java/*src.zip \
           /opt/java/include \
           /opt/java/db \
           /opt/java/bin \
           /opt/java/man \
           /opt/java/lib 

ENV JAVA_HOME /opt/java/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin

CMD ["java", "-version"]