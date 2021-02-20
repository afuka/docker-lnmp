FROM daocloud.io/library/nginx:${NGINX_VERSION}-alpine

ENV NGINX_VERSION="1.18"

### set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

