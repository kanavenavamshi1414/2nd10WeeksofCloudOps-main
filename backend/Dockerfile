# FROM node:20-alpine
# WORKDIR /app
# COPY package.json .
# RUN npm install --production
# COPY . .
# EXPOSE 80
# CMD ["node", "index.js"]

FROM maven:3.9.9-amazoncorretto-11 AS builder

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

FROM amazoncorretto:11-alpine-jdk

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8084

ENTRYPOINT ["java", "-jar", "app.jar"]
