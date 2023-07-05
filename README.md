# SpringBoot App with MongoDB and LB
+ Prince Chafah Forchu Sani # Kamstrup 3tier app demo
+ forchu.cha@gmail.com   # +4571573047
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
+ The cluster deploys the load balancer, the k8s master and worker nodes, the app and replicas, and the data with pv and PVC
```bash
kubectl apply -f springapp.yml
```
## Create Docker Image
+ A docker image is created with a linux apline base image.
+ The image is created using the Dockerfile
+ The image is pushed into a DockerHub repo
```docker
docker build -t chafah/springapp .
```
## List Docker Containers
```docker
docker ps -a
docker images
```
## Continous Integration and Deployment
+ Jenkins is used as the CI tool
+ It is integrated with Git to pull the app repo and for VC
+ Git webhook can be configured for automated builds
+ A Jenkinsfile is used for a pipeline job
+ Jenkins is integrated with Nexus, sonarqube, and necessary plugins installed
## Application Discovery and Access
+ To test if the application is running, you can run the following commands
```bash
kubectl get all #to see all resources
kubectl get pv # to get persistent volume
kubectl get node
kubectl get pods
kubectl get ep # to see if the diff apps can communicate with each other
kubectl get pvc #to get a persistent volume claim
```
+ The application can be accessed by either running the command
```bash
kubectl get svc
```
+ You can see how many nodes the application is running on by running the command
```bash
nslookup #loadbalancer url
```
+ using the service link which is an AWS load balancer OR,
+ Accessing AWS and copying the LB URL.
+ Using the AWS Route53 service, a DNS record can be created to provide a distributable app URL.
+ The current application url access is......It will run for a day since it is a paid service
```bash
http://a87bda1dcc7be4927a70e31a3dcfcae7-1517117890.us-east-2.elb.amazonaws.com/
```

## Liscence (forchu.cha@gmail.com)
