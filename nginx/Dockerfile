FROM alpine:latest

MAINTAINER n3wbiemember "<info@girirahayu.com>"

RUN set -x \
    && apk add --update --no-cache nginx tzdata

RUN ln -nsf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
RUN rm -fr /var/cache/apk/*

ADD nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /run/nginx
RUN mkdir -p /opt/app
RUN chown -R nobody:nobody /opt/app
WORKDIR /opt/app
ENTRYPOINT /usr/sbin/nginx -c /etc/nginx/nginx.conf -g 'daemon off;'
EXPOSE 80 443
