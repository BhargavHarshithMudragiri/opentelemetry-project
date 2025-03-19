#Setting Eclipse-Temurin as base image
FROM eclipse-temurin:21-jdk AS builder
#Setting the working directory
WORKDIR /usr/src/app
#Copying the gradle wrapper files
COPY gradlew* settings.gradle* build.gradle ./
COPY ./gradle ./gradle
#Downloading the gradle dependencies
RUN chmod +x ./gradlew
RUN ./gradlew 
RUN ./gradlew downloadRepos 
#Copying the source code
COPY . .
COPY ./pb ./proto
#Building the application
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

#Setting Eclipse-Temurin as release image
FROM eclipse-temurin:21-jre AS release
#Setting the working directory
WORKDIR /usr/src/app
#Copying the built application from the builder image
COPY --from=builder /usr/src/app/ ./
#Exposing the port
ENV AD_PORT=9099
EXPOSE $AD_PORT
#Running the application
ENTRYPOINT [ "./build/install/opentelemetry-demo-ad/bin/Ad" ]