#golang 1.14.2-alpine3.11
#recommeded always pulling image using digest
FROM golang@sha256:9b3ad7928626126b72b916609ad081cfb6c0149f6e60cef7fc1e9e15a0d1e973 AS builder
MAINTAINER n3wbiemember "<info@girirahayu.com>"

ARG REPO
ARG BRANCH

# Install git.
# Git is required for fetching the dependencies & sourcecode

RUN apk update && apk add --no-cache git

WORKDIR $GOPATH/src/

#tweak for disable cache
ARG CACHEBUST=1

RUN git clone $REPO app
RUN cekdir=`ls $DIR | wc -l` && \
    if [ $cekdir -gt 0 ]; then cd app && git checkout $BRANCH ; fi

WORKDIR $GOPATH/src/app
# Using go get.
RUN go get -d -v

#For small binnary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/main

#RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /go/bin/main
FROM scratch
COPY --from=builder /go/bin/main /
# Run the binary.
ENTRYPOINT ["/main"]
EXPOSE 8080
