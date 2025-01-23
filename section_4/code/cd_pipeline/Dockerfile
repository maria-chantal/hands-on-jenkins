# Base image
FROM alpine:3.18

# Set environment variables
ENV JENKINS_HOME=/home/jenkins

# Add the Jenkins user
RUN adduser -D -h "$JENKINS_HOME" -u 102 jenkins

# Add docker group and add Jenkins user to the group
RUN addgroup -g 497 docker && adduser jenkins docker

# Install necessary packages
RUN apk update && apk add --no-cache python3 py3-pip bash

# Upgrade pip
RUN pip3 install --upgrade pip

# Install Python modules needed by the app
COPY requirements.txt /usr/src/app/
RUN pip3 install --no-cache-dir -r /usr/src/app/requirements.txt

# Copy application files
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# Expose the port the app runs on
EXPOSE 5000

# Run the application
CMD ["python3", "/usr/src/app/app.py"]
