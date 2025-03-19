#Setting Python 3.12 as the base image
FROM python:3.12-slim-bookworm AS builder
#Setting the working directory
WORKDIR /usr/src/app
#Copying the requirements file
COPY requirements.txt .
#Installing the required packages
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
#Copying the source code
COPY . .
#Expose the port
ENV RECOMMENDATION_PORT=1011
EXPOSE ${RECOMMENDATION_PORT}
#Running the server
ENTRYPOINT [ "python", "recommendation_server.py" ]
