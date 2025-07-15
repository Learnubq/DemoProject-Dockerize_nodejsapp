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

<img width="598" height="164" alt="Dockerfile1" src="https://github.com/user-attachments/assets/d9e7d468-dbbf-4060-bec5-ca61281ffd1c" />


3. **Then executed this to confirm my Image was created:**

```bash
docker images
```

<img width="818" height="60" alt="Dockerfile2" src="https://github.com/user-attachments/assets/5aa49729-9514-495e-b223-4bdeca5b833a" />


4. **Then I ran a Docker container from the Docker Image:**

```bash
docker run my-app:1.0
```

<img width="990" height="55" alt="Dockerfile3" src="https://github.com/user-attachments/assets/c46c2b32-8d94-4b04-be2d-6c1bc7fd795f" />

5.**Then executed docker ps to check the app was running:**

```bash
docker ps
```

<img width="1294" height="56" alt="Dockerfile4" src="https://github.com/user-attachments/assets/f71b2707-7256-4e88-8136-2c13601ac606" />

6. **Then executed the following to see the Docker container logs:**

```bash
docker logs <containerID>
```

<img width="1296" height="64" alt="Dockerfile5" src="https://github.com/user-attachments/assets/f3dc52de-1ce9-47ef-8647-47822a5869f7" />

7. **Then executed this to get into the Docker container and get more insight about it:**

e.g. getting access to the CLI of the container terminal and looking around it

```bash
docker exec -it <containerID> /bin/sh
env
```

<img width="1716" height="109" alt="Dockerfile6" src="https://github.com/user-attachments/assets/f80e4930-4988-4850-a8ba-96607e662129" />


<img width="795" height="331" alt="Dockerfile7" src="https://github.com/user-attachments/assets/e330ae89-3336-4e90-b372-d92fa0f3991a" />

**If I had a hude application I would have needed to compress it and package it into an artifact, then copy the artifact into the Docker Image container.

8. **I created a Docker registry using AWS ECR:**

9. **I then executed Docker login to authenticate to AWS ECR after installing AWS CLI and configuring credentials:**

```bash
cd ~
<AWS docker login command>
```

10.**I then tagged my Docker Image and pushed it to the AWS ECR pricate registry:**

```bash
docker tag my-app:1.0 470633809269.dkr.ecr.eu-west-1.amazonaws.com/my-app:1.0
docker images
docker push 470633809269.dkr.ecr.eu-west-1.amazonaws.com/my-app:1.0
```

<img width="1306" height="275" alt="Dockerfile8" src="https://github.com/user-attachments/assets/e44a756a-4adb-4e77-8213-edaa90d00b28" />


**If you make any changes to any part of the Image contents, you will need to rebuild the Image and push again to the AWS ECR private repository.
**You can do the above and push as a new version number for the tag - it will allow you to push the new version to AWS ECR registry as it's not a completely different app. This is useful if testing.
**Docker login is done once per terminal session

