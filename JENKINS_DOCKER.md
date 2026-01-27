# Jenkins Docker Image with Sudo

This directory contains a Dockerfile for creating a Jenkins Docker image with sudo installed and configured for the jenkins user.

## Features

- Based on the official Jenkins LTS image
- Sudo package installed
- Jenkins user granted sudo privileges without password requirement
- Secure sudoers configuration

## Building the Image

To build the Jenkins Docker image:

```bash
docker build -f Dockerfile.jenkins -t jenkins-with-sudo .
```

## Running the Container

To run the Jenkins container:

```bash
docker run -p 8080:8080 -p 50000:50000 jenkins-with-sudo
```

## Verification

To verify that sudo is properly configured:

```bash
# Test sudo access
docker run --rm jenkins-with-sudo sudo whoami

# Check sudo permissions
docker run --rm jenkins-with-sudo sudo -l
```

## Security Considerations

The jenkins user has been granted NOPASSWD sudo access to all commands. In a production environment, you may want to:

1. Limit sudo access to specific commands only
2. Require password authentication for certain operations
3. Add additional security policies as needed

To customize the sudoers configuration, modify the following line in `Dockerfile.jenkins`:

```dockerfile
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/jenkins
```
