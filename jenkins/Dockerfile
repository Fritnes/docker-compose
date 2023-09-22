FROM jenkins/jenkins:lts
USER root
RUN apt update -y
RUN apt-get install software-properties-common -y
RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
RUN apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
RUN apt update -y
RUN apt install postgresql-client ansible wget zip terraform -y
