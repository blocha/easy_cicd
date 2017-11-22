FROM tomcat
MAINTAINER Tomasz Zabłocki <tomasz.zablocki@outlook.com>

RUN apt-get update && apt-get install -y openssh-server

#To allow jenkins to upload new apps
RUN useradd -m -s /bin/bash -p changeIt jenkins
RUN chown -R jenkins /usr/local/tomcat/webapps

RUN echo "jenkins:changeIt" | chpasswd
RUN sed -i 's/prohibit-password/yes/' /etc/ssh/sshd_config
RUN mkdir /home/jenkins/.ssh
RUN chown -R jenkins:jenkins /home/jenkins/.ssh;chmod -R 700 /home/jenkins/.ssh
RUN echo "StrictHostKeyChecking=no" >> /etc/ssh/ssh_config
RUN mkdir /var/run/sshd

COPY start.sh /start.sh
RUN chmod 755 /start.sh

CMD ["/start.sh"]


