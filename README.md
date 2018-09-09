# flask-app
This project is used to host python flask-app using docker. It also includes yaml Kubernetes assets for flask-app with technical documentation.

# Purpose
The aim of this repository is to house Docker-ized flask application. It is a internet facing application which has been designed for high availability using AWS resources.

# Access
Contact rsrahulsingh2030@gmail.com for queries related to access and code.

# Useful Docker links
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
* [Getting started with Docker](https://docs.docker.com/get-started/)

# Useful Kubernetes links
* [Kubernetes Documentation](https://kubernetes.io/docs/home/)
* [Run application in Kubernetes](https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/)

# Assignment specific links
* [Github](https://github.com/rsrahulsingh)
* [Dockerhub](https://hub.docker.com/r/rsrahulsingh/flask_image/)

# Structure
The repository's structure looks like:
```
|-----flask/
            |--Docker/
                |---web_applicaton.py
                |---requirements.txt
                |---Dockerfile
 
|-----------|--Kubernetes/
                |---deployment.yaml
                |---service.yaml
                |---eks/
				            |--kubeconfig.yaml
					          |--nodeconfig.yaml
					          |--nodegroup.yaml

|-----------|--Docs
                |---platformDesign.md
                |---kubernetes.md
                |---containerDesign.md 

 ``` 
 
 #Instruction to run docker container.

## Prerequisite.
* EC2 instance- Refer AWS official guide in order to find how to launch EC2 instance.
* User with root level privileges.

## Assumptions
* The application has inbuilt webserver. Hence there are no other internal web server or database. This architecture can be used for development purpose.
* The request is served on HTTP port using load balancer.


## Installation of Docker.
 Below steps are required to download and install docker.
```
yum -y update && -y yum upgrade
yum -y install wget
yum -y install http://mirror.centos.org/centos/7/extras/x86_64/Packages/container-selinux-2.42-1.gitad8f0f7.el7.noarch.rpm
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum -y install docker-ce
```
# Install git and pip
```
easy_install pip
yum install git
```
# Clone the git branch for application code and Docker file.
```
git clone https://github.com/rsrahulsingh/flask-app.git
```
# Build docker image
```
cd $HOME/flask-app/flask/Docker
docker build -t flaskv1:tag1 .
```
# Run the container
```
docker run -d -p 5000:5000 --name flaskv1c flaskv1:tag1
```

# Test the container service.
```
curl http://localhost:5000/
```

#Make changes to existing container by installing curl.
```
docker container exec -it CONTAINERID bash
apt-get install curl
exit
docker commit CONTAINERID REPO:TAG

```
# To tag and push the image to docker hub.
```
docker login
docker tag flaskv1:tag1 rsrahulsingh/flask_image:tagx
docker push rsrahulsingh/flask_image:tagx
```



# Design decision.

## Docker: Container engine

Docker is an open source project to pack, ship and run any application
as a lightweight container. They can run anywhere from laptop to  the EC2 compute instance and everything in between - and they don't require that we use a particular language, framework or packaging system. That makes them great building blocks for deploying and scaling web apps, databases and backend services without depending on a particular stack or provider.

Docker relies on a different sandboxing method known as containerization. Unlike traditional virtualization, containerization takes place at the kernel level. Most modern operating system kernels now support the primitives necessary for containerization.

## Key benefits:

* Return on investment and cost savings.
  Every management takes quick decision when return on investment is high. The more a solution can decrease cost of current system the more likely it is going to be adopted. Docker helps to dramatically reduce cost of infrastructure resources along with the people who manages those infra.  

* Standardization and productivity
  Docker containers ensures consistency across multiple development, release cycles and standardising the environment. Docker provides repeatable development, build, test, and production environments.

* CI efficiency
  Docker enables you to build a container image and use that same image across every step of the deployment process. A huge benefit of this is the ability to separate non-dependent steps and run them in parallel. 

* Isolation
  Docker ensures your applications and resources are isolated and segregated. Docker makes sure each container has its own resources that are isolated from other containers. You can have various containers for separate applications running completely different stacks. 

* Multi-Cloud Platforms
  This is possibly one of Docker’s greatest benefits. Over the last few years, all major cloud computing providers, including Amazon Web Services and Google Compute Platform, have embraced Docker’s availability and added individual support.


# Acknowledgments

The information shared has been referred from different sources like Docker official site, public blogs and Git.
