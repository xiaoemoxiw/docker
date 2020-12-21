from registry.cn-beijing.aliyuncs.com/hub-mirrors/openjdk:8-jdk-alpine
ARG JAR_FILE=target/application.jar
ARG ENV_APP_NAME

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

COPY  ./${ENV_APP_NAME}/${JAR_FILE} app.jar

ENTRYPOINT java -Djava.security.egd=file:/dev/./urandom -Dspring.profiles.active=test -jar /app.jar
