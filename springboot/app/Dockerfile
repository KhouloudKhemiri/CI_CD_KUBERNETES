# Étape 1 : compilation Maven (plus besoin de mvn en local)
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /build
COPY pom.xml .
RUN mvn -q dependency:go-offline
COPY src ./src
RUN mvn -q clean package -DskipTests

# Étape 2 : exécution (Java 17 minimum pour Spring Boot 3.3.x)
FROM eclipse-temurin:17-jre
EXPOSE 8081
COPY --from=build /build/target/demo-0.0.1.jar /app.jar
ENTRYPOINT ["java","-jar","/app.jar"]