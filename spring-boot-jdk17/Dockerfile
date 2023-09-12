FROM maven:3.9.0-eclipse-temurin-17-alpine AS MAVEN_BUILD

COPY pom.xml /build/
COPY src /build/src/

WORKDIR /build/
RUN mvn package

FROM eclipse-temurin:17-alpine

WORKDIR /app

COPY --from=MAVEN_BUILD /build/target/integrationAPI-1.0.0.jar /app/
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "integrationAPI-1.0.0.jar"]
