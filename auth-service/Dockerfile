FROM openjdk:8-jre-slim
COPY ./*.jar /app/auth-service.jar
CMD ["java", "-Xmx200m", "-jar", "/app/auth-service.jar"]

EXPOSE 5000
