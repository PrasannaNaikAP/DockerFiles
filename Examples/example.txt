# Example 1
------------------------------------------------------

# Use the official OpenJDK image as a base image
FROM openjdk:11-jre-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the .jar file from the host to the container
COPY myapp.jar /app/myapp.jar

# Expose the port your application runs on
EXPOSE 8080

# Command to run the .jar file
CMD ["java", "-jar", "/app/myapp.jar"]




# Example 2
------------------------------------------------------

FROM ubuntu

WORKDIR /app

COPY requirements.txt /app
COPY devops /app

RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install -r requirements.txt && \
    cd devops

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]


# Example 3
------------------------------------------------------


FROM ubuntu:latest

# Set the working directory in the image
WORKDIR /app

# Copy the files from the host file system to the image file system
COPY . /app

# Install the necessary packages
RUN apt-get update && apt-get install -y python3 python3-pip

# Set environment variables
ENV NAME World

# Run a command to start the application
CMD ["python3", "app.py"]
