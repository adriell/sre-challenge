FROM public.ecr.aws/docker/library/maven:3.9.9-amazoncorretto-23 AS builder

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests

FROM public.ecr.aws/docker/library/maven:3.9.9-amazoncorretto-23-alpine

RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-Djava.net.preferIPv4Stack=true", "-jar", "app.jar", "--server.address=0.0.0.0", "--server.port=${SERVER_PORT:-8080}"]