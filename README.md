# SpringBoot App with MongoDB and LB
## Application Architecture
+ The application has a basic 3tier architecture
+ FrontEnd, BackEnd, and Database
## FrontEnd
+ The frontend of the application is a k8s LoadBalancer
+ It acts as the user interface and routes traffic to various replicas of the application (nodes)
+ It is referred to as Service type LoadBalancer in the springapp.yml file to discover the application.
+ It can communicate with the application and not the database.
+ It is self-managed by the EKS

## BanckEnd
+ The backend of the application is the springboot Mongo App
+ It is designed to collect user input
+ The application is linked to the Mongodb and can write data into the database
+ The application can communicate with the LB and the database
+ The app has replicaSet which can manage the number of running replicas and can be scaled in and out depending on the app load
+ The number of worker nodes is managed by the AWS Autoscaling Group and can be automatically scaled using a policy

## DataBase
+ The database is MongoDB
+ It can communicate and collect data from the application by mapping the target port in the yml file to the app port
+ The database has volume persistency.
+ The db has a ReplicaSet with ensures that if the DB pod is destroyed, it will be automatically recreated with volume persistency

## Application Deployment and Hosting
+ The Application is hosted on AWS Cloud
+ The application is built using the Maven software as a defined dependency in the pom.xml file
  ```bash
  mvn clean package
  ```
+ The application is not tested but JUnit tests can be performed using sonarqube or Jacoco
 ```bash
sonar:sonar
```
+ Jar packages are created after build and can be uploaded into an artifactory like nexus
```bash
mvn deploy
```
+ The application is deployed using the AWS Elastic Kubernetes Service (EKS) which is a self-managed K8S cluster
+ The cluster deploys



# Build Project Using Maven

Maven is java based build tool to generate executable 

packages(jar, ear,war) for java based projects.

```bash
mvn clean package
```

## Create Docker Image
Docker is a continerization tool.Using docker we can deploy our applications as 

containes using docker images. Containers contains application code and also the softwares,

config files whatever is required for our application to run.

Create docker image using Dockerfile


```docker
docker build -t mylandmarktech/springapp .
```

## Deploy Application Using Docker Compose 

```docker-compose 
docker-compose up -d 
```

## List Docker Containers
```docker
docker ps -a
```
## License
[Landmark Technologies](http://www.mylandmarktech.com)
