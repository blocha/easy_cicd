FROM jenkins/jenkins:lts
MAINTAINER Tomasz Zabłocki <tomasz.zablocki@outlook.com>

# versions
ENV MAVEN_VERSION 3.5.2

USER root

# Maven
RUN mkdir -p /usr/share/maven \
	&& curl -fsSL https://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
	  | tar -xzC /usr/share/maven --strip-components=1 \
	&& ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven

# Some maven repo configuration
COPY settings.xml $MAVEN_HOME/conf/

# Make java run (gui tests)
RUN \
  apt-get update && apt-get install -y libxrender1 libxtst6 libxi6 && \
  rm -rf /var/lib/apt/lists/*

# Load jenkins plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Jenkins basic config
COPY config.xml /usr/share/jenkins/ref/
COPY credentials.xml /usr/share/jenkins/ref/
COPY com.dabsquared.gitlabjenkins.connection.GitLabConnectionConfig.xml /usr/share/jenkins/ref/
COPY org.jfrog.hudson.ArtifactoryBuilder.xml /usr/share/jenkins/ref/
COPY jenkins.plugins.publish_over_ssh.BapSshPublisherPlugin.xml /usr/share/jenkins/ref/
COPY org.jvnet.hudson.plugins.repositoryconnector.RepositoryConfiguration.xml /usr/share/jenkins/ref/
COPY hudson.tasks.Maven.xml /usr/share/jenkins/ref/
COPY jenkins.CLI.xml /usr/share/jenkins/ref/
COPY jobs /usr/share/jenkins/ref/jobs
COPY users /usr/share/jenkins/ref/users
COPY secrets /usr/share/jenkins/ref/secrets

USER jenkins

