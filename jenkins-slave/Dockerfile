FROM ubuntu:16.04

USER root

ENV DOTNET_RUNTIME_VERSION=2.2 \
    DOTNET_SDK_VERSION=2.2

# Install Docker CLI
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-engine

RUN apt-get update                                                          && \
    apt-get install -y --no-install-recommends wget ruby curl apt-transport-https gpg && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor     \
        > /etc/apt/trusted.gpg.d/microsoft.gpg                              && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" \
        > /etc/apt/sources.list.d/dotnetdev.list                            && \
    apt-get update                                                          && \
    apt-get install -y python python-pip                                    && \
    apt-get install -y --no-install-recommends dotnet-runtime-$DOTNET_RUNTIME_VERSION dotnet-sdk-$DOTNET_SDK_VERSION

USER jenkins