FROM ubuntu:22.04

# 필수 패키지 설치
RUN sed -i 's|http://archive.ubuntu.com/ubuntu/|http://kr.archive.ubuntu.com/ubuntu/|g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev git wget ffmpeg ca-certificates && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# nginx 소스 다운로드
WORKDIR /usr/src
RUN wget http://nginx.org/download/nginx-1.20.2.tar.gz && \
    tar zxvf nginx-1.20.2.tar.gz

# nginx_upstream_check_module 다운로드
RUN git clone https://github.com/yaoweibin/nginx_upstream_check_module.git

# nginx 빌드
WORKDIR /usr/src/nginx-1.20.2
RUN patch -p1 < ../nginx_upstream_check_module/check_1.20.1+.patch

RUN ./configure --prefix=/nginx/ \
				--conf-path=/nginx/conf/nginx.conf \
				--error-log-path=/nginx/logs/error.log \
				--http-log-path=/nginx/logs/access.log \
				--add-module=../nginx_upstream_check_module \
                --with-file-aio --with-threads --with-http_ssl_module \
    && make \
    && make install

# 포트 열기
EXPOSE 80

# 실행
CMD ["/nginx/sbin/nginx", "-g", "daemon off;"]
