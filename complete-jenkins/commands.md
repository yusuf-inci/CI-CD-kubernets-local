# Complete Jenkins Tutorial | Learn Jenkins From Scratch In 3 Hours 
- url: https://www.youtube.com/watch?v=nCKxl7Q_20I 

## Install Jenkins With war File
- be sure jdk 8 or jdk 11 installed
`apt install openjdk-11-jre-headless`
- run following command inside the folder war file stand
`java -jar jenkins.war`
- get the initial password and log in jenkins server via browser. on this case
`http://192.168.56.11:8080`
- configure user and install suggested plugins

## Install and Configure Maven Plugin
- Dashboard ==> Manage Jenkins ==> Global Tool Configuration ==> Maven installations ==> name: Maven3 
==> save
- Dashboard￼==> Manage Jenkins￼==> Plugin Manager ==> available ==> Maven Integration plugin ==> install

## Integration jenkins with Github

1. Integration Pre-Requisite
- GitHub must be able to send data to Jenkins
- Jenkins must have a public IP 
- Except for on-premise GitHub instances 

2. Github part add personal access token to jenkins instance
- goto github account ==> profile dropdown ==> select settings ==> navigate developer settings ==> personal access tokens ==> generate new token ==> name: jenkins ==> 
select scopes ==> check public repo ==> generate ==> grab the token value
- goto jenkins ==> manage jenkins ==> configure system ==> github section (comes from github plugin) ==> github server name: github ==> api url comes auto ==> credential 
==> add ==> jenkins credential providers page opens
- On add credential section kind: secret text ==> leave the scope as it is ==> secret: paste the personal access token value ==> ID: github-PAT ==> add
- On github section credentials dropdown shows new one (github-PAT) ==> select it and test the connection ==> uncheck Manage hooks (we configure it manually) ==> save

3. Create ssh-key pair ==> add public key to github ==> add private key to jenkins to allow clone down the repo to local jenkins workspace
- Create ssh-key pair: On jenkins open git bash session ==> enter `ssh-keygen` accept default ==> cat the public key ` cat ~/.ssh/id_rsa.pub` and grab it    
- add public key to github ==> goto github account ==> profile dropdown ==> select settings ==> SSH and GPG keys ==> new SSH Key ==> give a name for title ex: Jenkins Public Key ==> paste the public to Key section ==> hit Add SSH key 
- add private key to jenkins: cat the private key from git bash ` cat ~/.ssh/id_rsa ` and grab it ==> goto jenkins ==> manage jenkins ==> Security ==> Manage Credentials ==> select jenkins ==> select global ==> Add credential ==> kind: SSh Username with private key ==> leave the scope as it is ==> ID: github-private-key ==> Private key enter directly ==> paste the private key ==> ok

4. Create new job
- New item ==> test-job ==> free style project ==> ok ==> Source code management section select git ==> enter github repo SSH url ==> under credential section select user 
==> specify the branch ==> Under Build Trigers section check Github hook tri.... ==> Under Post Build Action Add Post build action hit Set HitHub commit status ==> under 
WHAT section status result hit One of default..... ==> Save
- goto repo ==> settings ==> navigate Webhooks ==> Add webhook ==> Payload URL: add jenkins base url ==> add github-webhook to url ==> ex: http.......:8080/github-webhook 
==> content type: application/json ==> choose the event that trigger this webhook ex:just push event ==> add webhook ==> be sure the test success ==> 
- test the job both commit on github and gitbash ==> check console output

## Create Jenkins Job for Maven project

1. Maven Project Job Type Refresher
- Maven Integration plugin provides a Maven Project job type ,
- Significantly reduces manual configuration.
- Test reporting in the jenkins interface

2. Create Maven project
- Source code: https://github.com/tech-with-moss/sample-maven-project.git
- Maven Quickstart url: https://maven.apache.org/archetypes/maven-archetype-quickstart/index.html
- goto jenkins Dashboard new item -- name: test-maven-project -- Maven Project -- OK
- configure source code management with SSH url
- configure Build Trigers -- consider Build whenever ... in this case check it -- consider Build after .. in this case uncheck -- consider Build periodically for every 
minute * * * * * in this case uncheck -- consider GitHub hook .... in this case check it -- consider Poll SCM (like opposite of hook) not a good practise, consuming 
resources in this case uncheck 
configure Build -- root pom -- goals and option : clean install -- Save

3. Add webhook to github repo
4. Build the project first time

## Configuring Jenkins Controller And Local Agent Node
1. The Problem 
- As software teams and their organizations grow, the need to scale Jenkins increases
- Software teams may need to test on multiple platforms
- A single Jenkins instance is insufficient
- Need to scale the Jenkins solution up and/or out

2. Adding Jenkins Controller and agent node for Windows
3. Adding Jenkins Controller and Jenkins agent node in Azure

## Understanding Jenkins Pipeline

1. Jenkins Pipeline Overview 
- Complex build and release processes can be difficult to manage using only freestyle jobs
- Jenkins Pipeline is a set of Jenkins plugins that allow you to model complex build and release processes as Groovy code in a file called “Jenkinsfile”

2. Pipeline Benefits
- Traceability and control of pipeline changes 
- Exist independent of a Jenkins instance
- Extensible through shared libraries and plugins
- Supports logic such as conditionals, loops, and parallel execution

3. Pipeline Terminology
- Pipeline: User-defined model of a build, test and release process for a software product
- Node: A machine that the Jenkins Controller can execute pipeline jobs on
- Stage: A logical grouping of steps that typically align with the build, test and release portions of the software development lifecycle
- Steps: Individual tasks completed within a stage of a pipeline (such as invoking a node's shell and executing a command such as “ls” or “mkdir" on it)

4. Install Pipeline Maven Integration Plugin

5. Create new job
- name: test-pipeline-job -- Pipeline -- OK -- go down pipeline section -- definition: pipeline script -- hit pipeline syntax
* in Script Generator, you can create individual step for a pipeline stage 
* in Declarative Directive Generator, you can create overall structure and stages of pipeline
- In script generation section select echo print message -- enter Hello World! -- hit generate pipeline script -- copy it and create new file on ide -- configure file with 
jenkins file structure -- goto job -- configure -- pipeline -- paste the script -- save and build pipeline