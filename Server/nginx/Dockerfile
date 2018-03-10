FROM centos
MAINTAINER walker Chan cylianging@163.com
RUN yum update
RUN yum install -y pcre pcre-devel
RUN yum install -y zlib zlib-devel
RUN yum install -y openssl openssl-devel
WORKDIR /home/Server
RUN yum install -y wget
RUN wget -c https://nginx.org/download/nginx-1.10.1.tar.gz
RUN tar -zxvf nginx-1.10.1.tar.gz
RUN mv nginx-1.10.1 nginx
WORKDIR /home/Server/nginx
RUN yum install -y gcc-c++
RUN ./configure
RUN make && make install
COPY nginx.conf /usr/local/nginx/conf/nginx.conf
ENV PATH=$PATH:/usr/local/nginx/sbin/
EXPOSE 80
CMD ["nginx"]


