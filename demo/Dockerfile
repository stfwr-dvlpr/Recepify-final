# Use a slim OpenJDK base image
FROM openjdk:21-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven wrapper and pom.xml to leverage Docker cache
COPY .mvn/ .mvn
COPY mvnw pom.xml ./

RUN chmod +x ./mvnw

# Download dependencies
RUN ./mvnw dependency:go-offline

# Copy the rest of the source code
COPY src ./src

# Package the application into a JAR file
# We skip tests to speed up the build process in this environment
RUN ./mvnw package -DskipTests

# Expose the port the app runs on
EXPOSE 8081

# Command to run the application
# Make sure to replace 'demo-0.0.1-SNAPSHOT.jar' with your actual JAR file name
CMD ["java", "-jar", "target/spring-boot-starter-parent-3.5.6.jar"]