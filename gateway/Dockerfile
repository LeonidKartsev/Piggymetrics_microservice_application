FROM openjdk:8-jre-slim
COPY ./*.jar /app/gateway.jar
CMD ["java", "-Xmx200m", "-jar", "/app/gateway.jar"]

EXPOSE 4000
