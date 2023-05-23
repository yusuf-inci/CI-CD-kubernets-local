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

12. Setting up Docker Cloud Agents
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> New Nodes: to create permanent agent. This is depracated way.
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> Configure clouds (This is how you set up agents using cloud platforms)
- go to plugin manager ==> install docker plugin ==> restart jenkins and log in again
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> Configure clouds ==> Add a new cloud ==> Add docker ==> follow number 13 below

13. Jenkins Agent using Docker Desktop fix  
- alpine/socat container to forward traffic from Jenkins to Docker Desktop on 
Host Machine
https://stackoverflow.com/questions/47709208/
how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
- goto terminal run following command
`docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/
run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr 
unix-connect:/var/run/docker.sock`
- grab the ip address
`docker inspect <container_id> | grep IPAddress`
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> Configure clouds ==> Add a new cloud ==> Add docker ==> Docker Host URI: tcp://container ip:2375
- check enabled ==> test connection ==> save

14. Docker Agent Template Setup 
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> Configure 
clouds ==> Add a new cloud ==> Add docker ==> Configure Clouds ==> Docker Agent Template ==> Add Docker Template ==> Labels: docker-agent-alpine ==> check enabled ==> name: docker-agent-alpine ==> docker image: jenkins/agent:alpine-jdk11 ==> instance capacity:2 ==> Remote file system: /home/jenkins ==> save

15. Using Labels to restrict Jobs to Agents 
- go to my-first-project and configure ==> check Restrict where this project can be run ==> label: docker-agent-alpine ==> save and build now ==> check the logs you'll see job run in the docker agent
- for the second job (my-python-job) we need the build new image ==> you can find dockerfile in python-image folder ==> run the following command in that folder to create and push the image
`docker build -t 90041/myjenkinsagents:python . && docker push 90041/myjenkinsagents:python`
- go to Dashboard ==> Manage Jenkins ==> Manage nodes and clouds ==> Configure 
clouds ==> Add a new cloud ==> Add docker ==> Configure Clouds ==> Docker Agent 
Template ==> Add Docker Template ==> Labels: docker-agent-python ==> check 
enabled ==> name: docker-agent-python ==> docker image: 90041/myjenkinsagents:python ==> instance capacity:2 ==> Remote file system: /home/jenkins ==> save 
- go to my-python-job and configure ==> check Restrict where this project can
be run ==> label: docker-agent-python ==> save and build now ==> check the logs 
you'll see job run in the docker agent 

16. Setting Builds to be automatically triggered on commits 
- go to my-python-job ==> Build triggers ==> check Poll SCM and schedule: */5 * * * * ==> save 
- make any change in the helloworld.py (print(" Hello world after enabled Poll SCM ") and commit&push it to repo and wait 5 minutes and check the log, you should see Started by an SCM change on top of console output.

17. Setting up Declarative Pipelines using Groovy
- Declarative pipeline using script:new item ==> pipeline ==> name: my_first_build_pipeline ==> ok ==> pipeline script ==> write the code ==> save and build ==> examine the logs

- Declarative pipeline using Groovy:new item ==> pipeline ==> name: 
my_first_build_pipeline ==> ok ==> pipeline script from SCM ==> SCM: Git ==> enter Repository url ==> enter script path ==> save and build ==> examine the logs ==> next time watch it will triger auto