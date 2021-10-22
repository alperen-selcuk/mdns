# TODO APP PROJECT

this project uses Java(11), Maven, Docker, Helm, Kubernetes, GitlabCI, Nginx Ingress, Google Cloud Platform


## 🚀 Languages and Tools:

<p align="left"> 
    <a href="https://www.java.com" target="_blank"> <img src="https://img.icons8.com/color/48/000000/java-coffee-cup-logo.png"/> </a>
    <a href="https://spring.io/projects/spring-boot" target="_blank"> <img src="https://img.icons8.com/color/48/000000/spring-logo.png"/> </a> 
    <a href="https://git-scm.com/" target="_blank"> <img src="https://img.icons8.com/color/48/000000/git.png"/> </a> 
    <a href="https://docs.gitlab.com/ee/ci/" target="_blank"> <img src="https://img.icons8.com/color/48/000000/gitlab.png"/> </a>
    <a href="https://maven.apache.org" target"_blank"> <img src="https://img.icons8.com/ios/50/000000/maven-ios.png"/> </a>
    <a href="https://docker.com" target"_blank"> <img src="https://img.icons8.com/color/48/000000/docker.png"/> </a>
    <a href="https://kubernetes.io" target"_blank"> <img src="https://img.icons8.com/color/48/000000/kubernetes.png"/> </a>
    <a href="https://nginx.com" target"_blank"> <img src="https://img.icons8.com/color/48/000000/nginx.png"/> </a>
    <a href="https://cloud.google.com" target"_blank"> <img src="https://img.icons8.com/color/48/000000/google-cloud.png"/> </a>
    
    
    
</p>

you can find details:

* Java: https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html
* Maven: https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html
* Docker: https://docs.docker.com/engine/installation/
* Helm: https://helm.sh
* Kubernetes: https://kubernetes.io/docs/tutorials/kubernetes-basics/


## Kubernetes Provisioning with Terraform

at the begining project we can provision Kubernetes cluster on Google Kubernetes Engine.

you can use this document: https://learn.hashicorp.com/tutorials/terraform/gke

![image](https://github.com/alperen-selcuk/mdns/blob/master/images/tf.gif?raw=true)

first type "terraform plan" for test our terraform files and after "terraform apply" to create kubernetes cluster. i have one kubernetes cluster now so i added only terraform plan command output as a gif.

## Project Structure

the below tree shows the basic project file structure.

![image](https://user-images.githubusercontent.com/78741582/138430969-2991c5fc-e469-4c24-8759-71aa1c578c50.png)


![image](https://user-images.githubusercontent.com/78741582/138431053-efab9ac9-5d8c-4111-b189-66e187f70f98.png)


## CI/CD structure

![image](https://user-images.githubusercontent.com/78741582/138431415-474f3ac3-cc54-4c4d-a08b-5b24d1b6f6a9.png)

project uses Gitlab CI for Continues Integration, uses Docker for Continues Delivery and uses Helm for Continues Deployment.

when has change and push master on repository frontend or backend gitlab start a pipeline with multiple jobs.

![image](https://user-images.githubusercontent.com/78741582/138440485-152c203d-22d0-4e7a-a4a7-02449090cc90.png)

* first stage, maven test, this job validate our java application can readdy to run. 
* seconda stage, maven build, this job compile our java application, install dependency and give us an artifact.
* third stage, build image, with Dockerfile build an image use existing artifact after that add commit id push dockerhub.
* fourth stage, build create helm chart for existing image tag.
* fifth stage, deploy helm chart on kubernetes cluster (dev namespace) with google sdk. 
* sixth stage, user interface test both frontend and backend. if http status is 200 pipeline success and continue
* last stage is prod deployment. this job trigger manually and deploy application prod namespace.

## Kubernetes Ingress 

both namespaces have got an ingress object. 

dev ingress has /todos path for backend to validate application is working on ui test stage.

below ingress use on prod namespace.


<script src="https://gist.github.com/alperen-selcuk/945eceb811a5b3d06c4c2b2b58804460.js"></script>
