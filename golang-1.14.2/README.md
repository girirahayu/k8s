# Build Example
docker build --build-arg REPO=https://github.com/girirahayu/gin-hello.git --build-arg BRANCH=master -t app:v1 .

# Docker Running
docker run -it -d --name appv1 -h app -p 80:8080 app:v1
