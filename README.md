
## Python_Dockerfile

Packaging the python environment

```bash
 # Dockerfile
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file and install dependencies
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]

  
```

## Java_Dockerfile

preparing for java environment

```bash

# Dockerfile
# Use an official OpenJDK runtime as a parent image
FROM openjdk:11-jre-slim

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the target directory to the container
COPY target/my-java-app.jar my-java-app.jar

# Expose the port the app runs on
EXPOSE 8080

# Run the Java application
CMD ["java", "-jar", "my-java-app.jar"]

```

## Npm_Dockerfile

Boundling the file for npm environment

```bash

# Dockerfile
# Step 1: Build the React app
FROM node:14 as build
WORKDIR /app
COPY client/package.json client/package-lock.json ./
RUN npm install
COPY client/ ./
RUN npm run build

# Step 2: Build the server
FROM node:14
WORKDIR /app
COPY server/package.json server/package-lock.json ./
RUN npm install
COPY server/ ./
COPY --from=build /app/build ./public

# Set environment variables if any
ENV NODE_ENV=production

# Expose the port the app runs on
EXPOSE 5000

# Run the server
CMD ["node", "index.js"]

```
## C++_Dockerfile

packaging environment for C++ application

```bash

# Dockerfile
FROM ubuntu:20.04

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    libgtest-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy the application files
WORKDIR /app
COPY . .

# Build the application
RUN mkdir -p build
RUN cd build && cmake .. && make

# Expose the port the app runs on
EXPOSE 8080

# Command to run the application
CMD ["./build/my-cpp-app"]

```
    
