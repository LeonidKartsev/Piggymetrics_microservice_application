FROM openjdk:8-jre-slim
COPY ./*.jar /app/registry.jar
CMD ["java", "-Xmx200m", "-jar", "/app/registry.jar"]

EXPOSE 8761
