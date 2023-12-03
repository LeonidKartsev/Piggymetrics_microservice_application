FROM openjdk:8-jre-slim
COPY ./*.jar /app/statistics-service.jar
CMD ["java", "-Xmx200m", "-jar", "/app/statistics-service.jar"]

EXPOSE 7000
