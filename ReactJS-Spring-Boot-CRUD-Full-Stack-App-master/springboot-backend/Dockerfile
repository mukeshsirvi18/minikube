# Use an image that includes Maven and OpenJDK for the builder stage
FROM maven:3.8.4-openjdk-11 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven project file (pom.xml) to the working directory
COPY . .
RUN mvn clean install -DskipTests=true

# Use a lightweight OpenJDK 11 image for the final stage
FROM openjdk:11-jre-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file built by Maven from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose port 8080 (or the port your Spring Boot app listens on)
EXPOSE 8080

# Command to run the Spring Boot application
CMD ["java", "-jar", "app.jar"]


