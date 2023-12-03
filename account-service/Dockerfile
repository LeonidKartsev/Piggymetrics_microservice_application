FROM openjdk:8-jre-slim
COPY ./*.jar /app/account-service.jar
CMD ["java", "-Xmx200m", "-jar", "/app/account-service.jar"]

EXPOSE 6000
