FROM cleafy/sxkdvm

ENV JENKINS_URL "http://jenkins:8080"
ENV JENKINS_AGENT_NAME "ios"

# installs Jenkins Agent
# based on https://github.com/jenkinsci/docker-slave/blob/master/Dockerfile
ENV HOME /home/jenkins
RUN groupadd -g 10000 jenkins
RUN useradd -c "Jenkins user" -d $HOME -u 10000 -g 10000 -m jenkins

ARG VERSION=3.16
ARG AGENT_WORKDIR=/home/jenkins/agent

RUN curl --create-dirs -sSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar

USER jenkins
ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /home/jenkins/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/jenkins/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/jenkins

# setups Jenkins connection
RUN wget https://raw.githubusercontent.com/jenkinsci/docker-jnlp-slave/master/jenkins-slave --output /usr/local/bin/jenkins-slave
ENTRYPOINT ["jenkins-slave"]
