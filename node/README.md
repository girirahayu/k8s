# Node Version available in alpine
 - 14.1.0
 - 13.14.0
 - 12.6.3
 - 10.20.1

## Build Docker
docker build --build-arg CACHEBUST=$(date +%s) \
--build-arg REPO=https://github.com/girirahayu/sample-language.git \
--build-arg BRANCH=node \
--build-arg NODE_VERSION=14.1.0 \
--build-arg INIT_SCRIPT=server.js -t node:v1 .

> if repo git using user/pass just change url to https://username:pass@github.com/resource/app.git

### Running Docker
docker run -d --name node -h node --restart=always -p 80:8080 node:v1 server.js

> server.js is init script for running the apps

