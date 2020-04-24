FROM jenkins/inbound-agent

USER root

ENV DOTNET_RUNTIME_VERSION=2.2 \
    DOTNET_SDK_VERSION=2.2

USER root

# Install the latest Docker CE binaries and add user `jenkins` to the docker group
RUN apt-get update && \
    apt-get -y --no-install-recommends install apt-transport-https \
      ca-certificates \
      curl \
      gnupg2 \
      software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
      $(lsb_release -cs) \
      stable" && \
   apt-get update && \
   apt-get -y --no-install-recommends install docker-ce && \
   apt-get clean
#   usermod -aG docker jenkins

RUN usermod -g docker jenkins
RUN usermod -a -G jenkins jenkins

#install dotnet core and sdk
RUN apt-get update                                                          && \
    apt-get install -y --no-install-recommends wget ruby curl apt-transport-https gpg && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor     \
        > /etc/apt/trusted.gpg.d/microsoft.gpg                              && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" \
        > /etc/apt/sources.list.d/dotnetdev.list                            && \
    apt-get update                                                          && \
    apt-get install -y python python-pip                                    && \ 
    apt-get install -y --no-install-recommends dotnet-runtime-$DOTNET_RUNTIME_VERSION dotnet-sdk-$DOTNET_SDK_VERSION

RUN pip install --no-cache-dir awscli

# drop back to the regular jenkins user - good practice
USER jenkins