# Commands

## Jenkins Infrastructure
### Master Server
- Controls Pipelines
- Schedules Builds

### Agents / Minions
- Perform the Build

### Agents Types
1. Permanent agent
- also known as a persistent agent or a long-lived agent, is an infrastructure agent that remains connected to the Jenkins master continuously.
- Dedicated Servers for Running jobs (install java, setup SSH, install build tool etc.)
2. Cloud Agents 
- Ephemeral/Dynamic Agents spun up on demand (Docker, Kubernetes, AWS Fleet Manager)


## YouTube Link
For the full 1 hour course watch out youtube:
https://www.youtube.com/watch?v=6YZvp2GwT0A

## Installation
1. Build the Jenkins BlueOcean Docker Image
`docker build -t myjenkins-blueocean:2.332.3-1 .`
2. Create the network 'jenkins'
`docker network create jenkins`
3. List docker network
`docker network ls`
4. Run the Container (MacOS / Linux)
```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.332.3-1
```
5. see the running docker container
`docker ps`
6. Open browser enter the following url `http://localhost:8080/`
7. Get the Password
`docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword`
8. Install suggested plugins
9. Creating a Simple Freestyle Job
- On Dashboard ==> New Item ==> Freestyle project ==> give a name for project ==> General tab ==> Build Section ==> Execute Shell
```
echo "Hello Jenkins"
echo "The build id of this job is ${BUILD_ID}"
echo "the build url of this job is ${BUILD_URL}"

ls -ltr

echo "1234" > test.txt

ls -ltr
```
- hit Save ==> Build now

10. Exploring the Jenkins Filesystem and Workspace
- go to terminal, login in to container. the volume we mounted is `/var/jenkins_home`. you'll see workspace directory in there. Once you build a job jenkins create a directory related your job in the workspace. Also plugins, updates, users, jobs, secrets and etc are in the jenkins users home directory. `cd ~` `ls -ltr`
`docker exec -it jenkins-blueocean bash`
`ls -ltra`

11. Freestyle job - Running Python scripts with Jenkins
- go to dashboard ==> New item ==> name: my-python-job freestyle project ==> Source Code Management ==> Git: <repository url> ==> Build ==> Execute shell ==> `python3 helloworld.py`==> save ==> build now 

12.



