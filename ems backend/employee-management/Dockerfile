# Stage 1: Build
FROM maven:3.9-eclipse-temurin-21 AS builder

WORKDIR /app

# Pehle sirf pom.xml copy karo, taaki dependencies cache ho jayein
COPY pom.xml .

RUN mvn dependency:go-offline -B

# Ab source code copy karke JAR banao
COPY src src

RUN mvn clean package -DskipTests


# Stage 2: Run
FROM eclipse-temurin:21-jre

WORKDIR /app

# Builder stage se JAR copy karo
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
