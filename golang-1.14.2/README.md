# Build Example

 - docker build --build-arg CACHEBUST=$(date +%s) --build-arg
   REPO=https://github.com/girirahayu/sample-language.git --build-arg
   BRANCH=master -t app:v1 .

    or

 - docker build --build-arg CACHEBUST=$(date +%s) --build-arg
   REPO=https://username:password@github.com/source/app.git
   --build-arg BRANCH=master -t app:v1 .

## Docker Running
docker run -it -d --name appv1 --restart=always -h app -p 80:8080 app:v1
