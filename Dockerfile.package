FROM airdock/oracle-jdk:latest

MAINTAINER Grissom Wang <grissom.wang@daocloud.io>

ENV TIME_ZONE Asia/Shanghai

RUN echo "$TIME_ZONE" > /etc/timezone

WORKDIR /app

RUN curl -o sources.list.jessie http://mirrors.163.com/.help/sources.list.jessie && mv sources.list.jessie /etc/apt/sources.list

RUN apt-get update

COPY target/zipkin-service-0.0.1-SNAPSHOT.jar /app/zipkin-service.jar

ENV JAVA_OPTS="-Dfile.encoding=UTF-8 -Duser.timezone=Asia/Shanghai -server -Xms3072m -Xmx3072m -XX:MaxNewSize=512m -XX:PermSize=512m -XX:MaxPermSize=512m -Djava.awt.headless=true -XX:-UseGCOverheadLimit -XX:+HeapDumpOnOutOfMemoryError"

EXPOSE 8080

EXPOSE 8081

ENTRYPOINT [ "sh", "-c", "java -jar $JAVA_OPTS -Dspring.profiles.active=prod zipkin-service.jar" ]