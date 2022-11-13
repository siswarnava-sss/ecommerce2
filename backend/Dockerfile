# TODO
#FROM openjdk:11 as buildstage
#WORKDIR /app
#COPY mvnw .
#COPY mvnw.cmd .
##COPY .mvn .mvn
#COPY pom.xml .
#COPY src src
#RUN mvn package
# FROM eclipse-temurin:17-jdk-focal as buildstage

# WORKDIR /app

# #COPY .mvn .mvn
# COPY mvnw pom.xml ./
# RUN ./mvnw dependency:go-offline

# COPY src ./src
# COPY target/*.jar app.jar

# FROM openjdk:11
# COPY --from=buildstage /app/app.jar .


FROM maven AS build
COPY src /usr/src/app/src
COPY pom.xml /usr/src/app
RUN mvn -f  /usr/src/app/pom.xml clean package -DskipTests=true

FROM openjdk:11
COPY --from=build /usr/src/app/target/*.jar app.jar 
ENTRYPOINT ["java", "-jar","app.jar", "--spring.profiles.active=docker"]
