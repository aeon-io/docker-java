FROM aeonproject/base
MAINTAINER 'Aeon Builds <builds+dockerfile@aeon.io>'

ENV GLIBC_VERSION      2.23-r1
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 77
ENV JAVA_VERSION_BUILD 03
ENV JAVA_PACKAGE       server-jre

WORKDIR /tmp

RUN apk add --no-cache --update-cache bash curl ca-certificates \
 && curl -Lo /etc/apk/keys/andyshinn.rsa.pub "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/andyshinn.rsa.pub" \
 && curl -Lo glibc-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk" \
 && curl -Lo glibc-bin-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk" \
# && curl -Lo glibc-i18n-${GLIBC_VERSION}.apk "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-i18n-${GLIBC_VERSION}.apk" \
 && apk add glibc-${GLIBC_VERSION}.apk glibc-bin-${GLIBC_VERSION}.apk \
# && apk add glibc-i18n-${GLIBC_VERSION}.apk \
 && mkdir -p /opt/java \
 && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" \
    "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz" | \
    tar -xzf - -C /opt \
 && mv /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR}/jre /opt/java/jre \
 && rm /opt/java/jre/bin/jjs \
 && rm /opt/java/jre/bin/keytool \
 && rm /opt/java/jre/bin/orbd \
 && rm /opt/java/jre/bin/pack200 \
 && rm /opt/java/jre/bin/policytool \
 && rm /opt/java/jre/bin/rmid \
 && rm /opt/java/jre/bin/rmiregistry \
 && rm /opt/java/jre/bin/servertool \
 && rm /opt/java/jre/bin/tnameserv \
 && rm /opt/java/jre/bin/unpack200 \
 && rm /opt/java/jre/lib/ext/nashorn.jar \
 && rm /opt/java/jre/lib/jfr.jar \
 && rm -rf /opt/java/jre/lib/jfr \
 && rm -rf /opt/java/jre/lib/oblique-fonts \
 && rm -rf /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} \
 && apk del curl ca-certificates \
 && rm -rf /tmp/* /var/cache/apk/* \
 && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

ENV JAVA_HOME /opt/java/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin

WORKDIR /

CMD ["java", "-version"]