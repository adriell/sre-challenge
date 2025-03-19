FROM public.ecr.aws/amazoncorretto/21 AS builder

WORKDIR /app

RUN yum install -y maven

COPY . .
RUN mvn clean package -DskipTests

FROM public.ecr.aws/amazoncorretto/21-alpine

RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]