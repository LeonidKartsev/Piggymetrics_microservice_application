FROM openjdk:8-jre-slim
COPY ./*.jar /app/notification-service.jar
CMD ["java", "-Xmx200m", "-jar", "/app/notification-service.jar"]

EXPOSE 8000
