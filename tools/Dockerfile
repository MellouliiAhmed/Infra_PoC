# Use the official Jenkins base image
FROM jenkins/jenkins:jdk17

# Switch to root user to install Docker
USER root

# Update the package list and install necessary packages
RUN apt-get update \
    && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

# Add Docker's official GPG key
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

# Add Docker's stable repository
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable"

# Update the package list again and install Docker
RUN apt-get update \
    && apt-get install -y docker-ce docker-ce-cli containerd.io

# Add Jenkins user to the Docker group
RUN usermod -aG docker jenkins

# Switch back to the Jenkins user
USER jenkins

# Expose the default Jenkins port
EXPOSE 8080

# # Run Jenkins
# ENTRYPOINT ["/usr/bin/tini" "--" "/usr/local/bin/jenkins.sh"]

# Use the default Jenkins entrypoint
CMD ["/usr/local/bin/jenkins.sh"]