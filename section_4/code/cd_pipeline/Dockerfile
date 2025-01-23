# base image
FROM alpine:3.18

# add user jenkins
RUN useradd -d "$JENKINS_HOME" -u 102 -m -s /bin/bash jenkins

# Create docker group with gid = 497 and add jenkins to the group
# This will allow the jenkins user to run docker commands
RUN groupadd -g 497 docker && \
    usermod -a -G docker jenkins \

# Install python 3 and pip
RUN apk add --no-cache python3 py3-pip

# Install Python modules needed by the Python app
COPY requirements.txt /usr/src/app/
RUN pip3 install --upgrade pip
RUN pip3 install --no-cache-dir -r /usr/src/app/requirements.txt

# Copy files required for the app to run
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# Tell the port number the container should expose
EXPOSE 5000

# Run the application
CMD ["python3", "/usr/src/app/app.py"]
