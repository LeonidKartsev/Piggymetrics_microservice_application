FROM openjdk:8-jre-slim
COPY ./*.jar /app/turbine-stream-service.jar
CMD ["java", "-Xmx200m", "-jar", "/app/turbine-stream-service.jar"]

EXPOSE 8989
