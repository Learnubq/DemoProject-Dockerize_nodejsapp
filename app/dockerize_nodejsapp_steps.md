## Demo Project - Dockerize Nodejs Application and Push to Private Docker Registry

This demo shows the process of buidling a Docker Image that has a Nodejs application packaged into it, and then pushing that Docker Image to a private Docker registry.

## Technologies Used
- Docker
- Node.js
- Amazon ECR

## Steps to Dockerize Nodejs Application and Push to Private Docker Registry

1. **Created a new Dockerfile and assigned RUN, ENTRYPOINT and ENV variable commands:**

```bash
vim Dockerfile
```

2. **Ran the following command within the project directory to build the Image from the Dockerfile:**

```bash
docker build -t my-app:1.0 .
```

3. **Then executed this to confirm my Image was created:**

```bash
docker images
```

4. **Then I ran a Docker container from the Docker Image:**

```bash
docker run my-app:1.0
```

5.**Then executed docker ps to check the app was running:**

```bash
docker ps
```
6. **Then executed the following to see the Docker container logs:**

```bash
docker logs <containerID>
```

7. **Then executed this to get into the Docker container and get more insight about it:**

e.g. getting access to the CLI of the container terminal and looking around it

```bash
docker exec -it <containerID> /bin/sh
env
```
**If I had a hude application I would have needed to compress it and package it into an artifact, then copy the artifact into the Docker Image container.

8. **I created a Docker registry using AWS ECR:**

9. **I then executed Docker login to authenticate to AWS ECR after installing AWS CLI and configuring credentials:**

```bash
cd ~
<AWS docker login command>
```

10.**I then tagged my Docker Image:**

```bash
docker tag my-app:1.0 470633809269.dkr.ecr.eu-west-1.amazonaws.com/my-app:1.0
docker images
docker push 470633809269.dkr.ecr.eu-west-1.amazonaws.com/my-app:1.0
```

**If you make any changes to any part of the Image contents, you will need to rebuild the Image and push again to the AWS ECR private repository.
**You can do the above and push as a new version number for the tag - it will allow you to push the new version to AWS ECR registry as it's not a completely different app. This is useful if testing.
**Docker login is done once per terminal session

