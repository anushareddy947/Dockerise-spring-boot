FROM maven:3.6.1-jdk-8-slim
ARG WORK_DIR=/backend-application
ENV WORK_DIR ${WORK_DIR}
RUN mkdir ${WORK_DIR}
WORKDIR ${WORK_DIR}
COPY pom.xml ${WORK_DIR}
RUN mvn clean install
RUN mvn clean package
RUN mvn spring-boot:run 
#RUN mvn -f pom.xml clean package
FROM openjdk:16.0.1
ADD target/spring-boot-angular-1.0.jar spring-boot-angular-1.0.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "spring-boot-angular-1.0.jar"]

