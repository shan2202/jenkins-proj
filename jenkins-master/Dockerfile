# Starting off with the Jenkins base Image
FROM jenkins/jenkins:latest

USER root

ENV JENKINS_REF /usr/share/jenkins/ref

# Installing the plugins we need using the in-built install-plugins.sh script
# COPY jenkins-home/plugins.txt $JENKINS_REF/plugins/
# RUN /usr/local/bin/plugins.sh $JENKINS_REF/plugins/plugins.txt
RUN /usr/local/bin/install-plugins.sh git matrix-auth workflow-aggregator docker-workflow blueocean credentials-binding
# RUN /usr/local/bin/install-plugins.sh $(cat $JENKINS_REF/plugins/plugins.txt | tr '\n' ' ')
# RUN /usr/local/bin/install-plugins.sh < $JENKINS_REF/plugins.txt

# Setting up environment variables for Jenkins admin user
ENV JENKINS_USER admin
ENV JENKINS_PASS password

# Skip the initial setup wizard
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Start-up scripts to set number of executors and creating the admin user
COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/

VOLUME /var/jenkins_home

USER jenkins