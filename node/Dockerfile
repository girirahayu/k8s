#node 14.1.0-alpine.3.11
#FROM node@sha256:00557fd939b1b87d0cd240c84aad62b77efc75146892f3e60117a6a696223f16 

ARG NODE_VERSION
FROM node:$NODE_VERSION-alpine3.11
MAINTAINER n3wbiemember "<info@girirahayu.com>"


ARG REPO
ARG BRANCH

RUN apk update && apk add --no-cache git

#tweak for disable cache
ARG CACHEBUST=1

WORKDIR /opt/

RUN git clone $REPO app
RUN cekdir=`ls $DIR | wc -l` && \
    if [ $cekdir -gt 0 ]; then cd app && git checkout $BRANCH ; fi

WORKDIR /opt/app/
RUN npm install

#CLEAN
RUN set -x && apk del git && rm -fr /var/cache/apk/*

CMD ["/usr/local/bin/node"]
EXPOSE 8080
