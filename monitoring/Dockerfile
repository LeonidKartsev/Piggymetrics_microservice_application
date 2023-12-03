FROM openjdk:8-jre-slim
COPY ./*.jar /app/monitoring.jar
CMD ["java", "-Xmx200m", "-jar", "/app/monitoring.jar"]

EXPOSE 8080
