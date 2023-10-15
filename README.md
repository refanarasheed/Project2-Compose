# Jenkins Docker Image with Docker and Plugins

This Dockerfile sets up a custom Jenkins environment based on the official Jenkins image (jenkins/jenkins:2.414.2-jdk17). It includes Docker and specific Jenkins plugins.

## Usage

1. **Build the Docker Image**

    Build the Docker image using the following command:

    ```
    docker build -t jenkins_docker .
    ```

2. **Run the Docker Container**

    Start a container from the image, ensuring it's properly configured and runs Jenkins with the specified plugins:

    ```
    docker run --name jenkins-blueocean --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro --volume ~/host_home:/home --restart=on-failure --env JAVA_OPTS="-Dhudson.plugins.git.GitSCM.ALLOW_LOCAL_CHECKOUT=true" --publish 8080:8080 --publish 50000:50000 jenkins_docker
    ```

3. **Access Jenkins**

    Once the container is running, you can access Jenkins by navigating to [http://localhost:8080](http://localhost:8080) in your web browser.

4. **Initial Unlock**

    During the first access, Jenkins will require you to unlock it using an initial admin password. You can find this password in the container logs by running:

    ```
   docker logs jenkins-blueocean
    ```

5. **Login and Configuration**

    - Log in to Jenkins with the admin password.
    - Customize your Jenkins environment, install additional plugins, and configure it as needed.
    - The Docker client is already set up within the container, allowing you to interact with Docker directly.

## Customization

For more information on Jenkins and its configuration, refer to the [Jenkins Documentation](https://www.jenkins.io/doc/).

---
