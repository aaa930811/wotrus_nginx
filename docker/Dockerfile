FROM debian:11-slim as build
ADD nginx-1.24.0.tar.gz /root/
ADD wotrus_ssl.tar.gz /usr/local/
WORKDIR /root/nginx-1.24.0/
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
 apt update && \
 apt install -y build-essential && \
 apt install -y gcc make libpcre3 libpcre3-dev  && \
 sed -in "s/\.openssl\///g" auto/lib/openssl/conf && \
 ./configure --without-http_gzip_module --with-http_ssl_module --with-http_stub_status_module --with-http_v2_module --with-file-aio --with-openssl="/usr/local/wotrus_ssl" --with-cc-opt="-I/usr/local/wotrus_ssl/include" --with-ld-opt="-lm" && \
 make install && \
 mkdir /usr/local/nginx/conf/conf.d && \
 mkdir /usr/local/nginx/conf/ssl && \
 sed -i '$i  \    include /usr/local/nginx/conf/conf.d/*.conf;' /usr/local/nginx/conf/nginx.conf

FROM debian:11-slim
COPY --from=build /usr/local/nginx/ /usr/local/nginx/

EXPOSE 80 443
VOLUME ["/usr/local/nginx/conf/conf.d/","/usr/local/nginx/conf/ssl/"]
CMD ["/usr/local/nginx/sbin/nginx","-g","daemon off;"]