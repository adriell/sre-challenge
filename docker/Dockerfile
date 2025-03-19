FROM maven:3.9.9-amazoncorretto-23 AS builder

WORKDIR /app

COPY ./app .
RUN mvn clean package -DskipTests

FROM maven:3.9.9-amazoncorretto-23-alpine

RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]