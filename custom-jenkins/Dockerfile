FROM jenkins/jenkins
USER root
#Install Docker
RUN apt-get update
RUN apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update
RUN apt-get -y install docker-ce=17.12.1~ce-0~debian
#install Node
RUN sudo apt-get install curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
RUN sudo apt-get install nodejs
RUN npm install -g --save-dev @angular-devkit/build-angular
RUN npm install -g --save-dev http-server
RUN npm install -g @angular/cli
#Install Google Chrome (Required for selenium)
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN sudo apt -y install ./google-chrome-stable_current_amd64.deb
#Install Allure (To view selenium report)
RUN curl http://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline/2.10.0/allure-commandline-2.10.0.tgz -o allure.tgz
RUN tar -xvzf allure.tgz
RUN mv allure-2.10.0 /opt/allure
WORKDIR /app
COPY . /app
RUN /usr/local/bin/install-plugins.sh < jenkins-plugin.list
RUN usermod -aG docker jenkins

