FROM debian:latest
LABEL mainteiner="begemot"

USER root
RUN apt-get update && apt-get upgrade
RUN apt-get install -y curl wget telnet net-tools less nano procps supervisor php7.0 php-fpm build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev
RUN rm -rf /root/nginx && mkdir /root/nginx && curl https://nginx.org/download/nginx-1.15.3.tar.gz | tar -xzC /root/nginx
RUN cd /root/nginx/nginx-1.15.3 && ./configure
RUN cd /root/nginx/nginx-1.15.3 && ./configure --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module --with-http_v2_module && make && make install
RUN touch /var/run/nginx.pid
COPY keep_container.sh /root/keep_container.sh
EXPOSE 443/tcp
CMD ["/bin/bash", "-c", "/root/keep_container.sh"]
