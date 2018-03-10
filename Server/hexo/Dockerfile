FROM centos
MAINTAINER walker Chan cylianging@163.com
RUN yum update
RUN yum install wget -yqq
WORKDIR /home/Server
RUN wget https://nodejs.org/dist/v6.11.2/node-v6.11.2-linux-x64.tar.xz --no-check-certificate
RUN tar -xvf node-v6.11.2-linux-x64.tar.xz
RUN mv node-v6.11.2-linux-x64 node
ENV PATH=$PATH:/home/Server/node/bin
RUN npm install -g hexo-cli
RUN hexo init blog
WORKDIR blog
COPY _config.yml ./
RUN npm install -save hexo-admin
EXPOSE 4000
