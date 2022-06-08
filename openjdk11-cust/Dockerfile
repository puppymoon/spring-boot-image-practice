FROM eclipse-temurin:11-jdk-alpine as jre-build

ARG JAR_FILE=*.jar
COPY ${JAR_FILE} /app/app.jar
RUN mkdir /app/unpacked && \
    cd /app/unpacked && \
    unzip ../app.jar && \
    cd .. && \
    $JAVA_HOME/bin/jdeps \
    --ignore-missing-deps \
    --print-module-deps \
    -q \
    --recursive \
    --multi-release 17 \
    --class-path="./unpacked/BOOT-INF/lib/*" \
    --module-path="./unpacked/BOOT-INF/lib/*" \
    ./app.jar > /deps.info && \
 $JAVA_HOME/bin/jlink \
 --add-modules $(cat /deps.info) \
 --strip-debug \
 --no-man-pages \
 --compress=2 \
 --output /javaruntime

FROM alpine:latest
ENV JAVA_HOME=/opt/java/openjdk
ENV PATH "${JAVA_HOME}/bin:${PATH}"
COPY --from=jre-build /javaruntime $JAVA_HOME
ARG JAR_FILE=*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
