FROM        --platform=$TARGETOS/$TARGETARCH container-registry.oracle.com/os/oraclelinux:8-slim

LABEL       author="AlexProgrammerDE"

LABEL       org.opencontainers.image.source="https://github.com/AlexProgrammerDE/yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN microdnf update -y oraclelinux-release-el8 \
    && microdnf --enablerepo ol8_codeready_builder install bzip2-devel ed gcc gcc-c++ gcc-gfortran gzip file fontconfig less libcurl-devel make openssl openssl-devel readline-devel tar glibc-langpack-en \
    vi which xz-devel zlib-devel findutils glibc-static libstdc++ libstdc++-devel libstdc++-static zlib-static curl ca-certificates git sqlite freetype tzdata iproute ipset \
    && microdnf clean all \
	&& useradd -d /home/container -m container

RUN fc-cache -f -v

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

ENV JAVA_HOME /graalvm
ENV PATH $JAVA_HOME/bin:$PATH

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]