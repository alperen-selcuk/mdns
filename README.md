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
* fourth stage, build create helm chart for existing image tag. push chartmuseum as tgz file.
* fifth stage, deploy helm chart on kubernetes cluster (dev namespace) with google sdk. 
* sixth stage, user interface test both frontend and backend. if http status is 200 pipeline success and continue
* last stage is prod deployment. if everyting is ok, this job trigger manually by QA engineer or devops and deploy application prod namespace. i think every pipeline should have control mechanism so i put this stage.


## Kubernetes Ingress 

both namespaces have got an ingress object. 

dev ingress has /todos path for backend to validate application is working on ui test stage.

below ingress use on prod namespace.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: todo-app
  namespace: prod
  annotations:
spec:
  ingressClassName: nginx
  rules:
  - host: "YOUR URL"
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: frontend
            port:
              number: 8080

```

## Grafana 

if you want see pods metric you can use grafana operator.

![image](https://user-images.githubusercontent.com/78741582/138460012-824f5dee-323b-4002-a3ca-4b63a0dc2b7a.png)

```
kubectl create ns monitoring
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring




```

## Conclusion


this pipeline work properly. you can reach prod application gui use that link http://todoprod-34-145-56-240.nip.io 

you can see my path for this project i tried first :)

![image](https://user-images.githubusercontent.com/78741582/138456855-6c105988-8691-4b84-8f8c-109cd3ad4bbd.png)




you can touch me whenever you want below platforms.

<p
    <a href="https://www.linkedin.com/in/hasan-alperen-selçuk-529a8a4a/" target"_blank"> <img src="https://img.icons8.com/color/48/000000/linkedin.png"/> </a>
     <a href="https://alperenhasanselcuk.medium.com" target"_blank"> <img src="https://img.icons8.com/color/48/000000/medium-logo--v2.png"/> </a>
</p>

