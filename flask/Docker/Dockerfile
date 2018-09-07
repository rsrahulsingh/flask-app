#This dockerfile is used to create python flask application using ubuntu base image.
FROM ubuntu:latest
# Maintainer of the file.
MAINTAINER rahul singh "rsrahulsingh2030@gmail.com"
# Install python and dependencies.
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
# Add the code to the app directory.
COPY . /app
# Set the working directory.
WORKDIR /app
# Install the flask module.
RUN pip install -r requirements.txt
#Run the application
CMD ["python","web_application.py"]