FROM aeonproject/base
MAINTAINER 'Aeon Builds <builds+dockerfile@aeon.io>'

ENV GLIBC_VERSION      2.23-r1
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 74
ENV JAVA_VERSION_BUILD 02
ENV JAVA_PACKAGE       jdk

WORKDIR /tmp

RUN apk add --no-cache --update-cache bash curl ca-certificates \
 && curl -Lo /etc/apk/keys/andyshinn.rsa.pub "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/andyshinn.rsa.pub" \
 && curl -Lo glibc-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk" \
 && curl -Lo glibc-bin-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk" \
# && curl -Lo glibc-i18n-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-i18n-${GLIBC_VERSION}.apk" \
 && apk add glibc-${GLIBC_VERSION}.apk glibc-bin-${GLIBC_VERSION}.apk \
# && apk add glibc-i18n-${GLIBC_VERSION}.apk
 && mkdir /opt \
 && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" \
    http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \
    | tar -xzf - -C /opt \
 && ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/java \
 && rm -rf /opt/java/*src.zip \
           /opt/java/lib/missioncontrol \
           /opt/java/lib/visualvm \
           /opt/java/lib/*javafx* \
           /opt/java/jre/bin/javaws \
           /opt/java/jre/lib/plugin.jar \
           /opt/java/jre/lib/ext/jfxrt.jar \
           /opt/java/jre/lib/javaws.jar \
           /opt/java/jre/lib/desktop \
           /opt/java/jre/lib/deploy* \
           /opt/java/jre/lib/*javafx* \
           /opt/java/jre/lib/*jfx* \
           /opt/java/jre/lib/amd64/libdecora_sse.so \
           /opt/java/jre/lib/amd64/libprism_*.so \
           /opt/java/jre/lib/amd64/libfxplugins.so \
           /opt/java/jre/lib/amd64/libglass.so \
           /opt/java/jre/lib/amd64/libgstreamer-lite.so \
           /opt/java/jre/lib/amd64/libjavafx*.so \
           /opt/java/jre/lib/amd64/libjfx*.so \
           /opt/java/jre/plugin \
           /tmp/*

ENV JAVA_HOME /opt/java
ENV PATH ${PATH}:${JAVA_HOME}/bin

WORKDIR /

CMD ["java", "-version"]
