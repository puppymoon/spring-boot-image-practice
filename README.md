# spring-boot-image-practice

build alpine jdk8 image
```
docker build -t spring-boot-image:jdk8 ./openjdk8/
```
build alpine jdk11 image
```
docker build -t spring-boot-image:jdk11 ./openjdk11/
```
build alpine customer jdk11 image
```
docker build -t spring-boot-image:jdk11-cust ./openjdk11-cust/
```

check size between images
```
docker images
```

run container
```
docker run -itd -p 8080:8080 spring-boot-image:jdk11-cust
```

check service status
```
curl localhost:8080
#Hello Docker World
```
