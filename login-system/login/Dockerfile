# Use a lightweight OpenJDK base image for Java 17
# This image is suitable for running Spring Boot applications
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Define an argument for the JAR file name.
# This makes the Dockerfile more flexible if your JAR name changes.
# The default value assumes the standard Spring Boot JAR naming convention.
ARG JAR_FILE=target/*.jar

# Copy the built JAR file from your Jenkins workspace (host) into the container.
# The JAR_FILE argument will resolve to the actual JAR path, e.g., target/login-0.0.1-SNAPSHOT.jar
# This assumes your Jenkins build stage 'Package Final JAR with Frontend' has already
# placed the final JAR (which includes the React static files) in the 'target/' directory
# relative to the backend project root.
COPY ${JAR_FILE} app.jar

# Expose the port that your Spring Boot application will run on.
# We're setting it to 8085 as discussed, to avoid conflict with Jenkins' 8080.
EXPOSE 8085

# Define the command to run your Spring Boot application when the container starts.
# We explicitly set the server.port here, which will override any port configured
# in application.properties/yml, making the Docker container self-contained for its port.
ENTRYPOINT ["java", "-jar", "app.jar", "--server.port=8085"]

