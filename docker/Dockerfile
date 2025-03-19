# Definindo a variável de ambiente JAVA_OPTS no Dockerfile
ENV JAVA_OPTS="-Djava.net.preferIPv4Stack=true"

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

CMD ["java", "$JAVA_OPTS", "-jar", "app.jar"]