#golang 1.14.2-alphine3.11


MAINTAINER n3wbiemember "<info@girirahayu.com>"
FROM sha256:9b3ad7928626126b72b916609ad081cfb6c0149f6e60cef7fc1e9e15a0d1e973 AS builder

ARG REPO
ARG BRANCH

# Install git.
# Git is required for fetching the dependencies & sourcecode

RUN apk update && apk add --no-cache git

WORKDIR $GOPATH/src/package/
RUN git clone $REPO app
RUN cekdir=`ls $DIR | wc -l` && \
    if [ $cekdir -gt 0 ]; then cd app && git checkout $BRANCH ; fi

WORKDIR $GOPATH/src/package/app
# Using go get.
RUN go get -d -v

RUN GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/main

FROM scratch
COPY --from=builder /go/bin/main /go/bin/main

# Run the hello binary.
ENTRYPOINT ["/go/bin/main"]
