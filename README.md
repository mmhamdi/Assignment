# Project Name

Brief description of your project.

## Table of Contents

- [Introduction](#introduction)
- [Architecture](#architecture)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Provide an overview of your project, its purpose, and the problem it aims to solve. Explain the importance and relevance of the project within its context.

## Architecture
![Alt Text](images/architecture.drawio.png)


## Features

List and describe the key features of your project. You can also include any notable functionalities or capabilities.

## Installation


### Prerequisites

A system running  Ubuntu 20.04
2 CPUs or more
2GB of free memory
20GB of free disk space

### Installation minikube cluster 

Step 1: Update System and Install Required Packages:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```
 install (or check whether you already have) the following required packages:
 
```bash
sudo apt-get install curl
sudo apt-get install apt-transport-https
```
Step 2:install docker :
   Set up Docker's apt repository:
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Install the Docker packages:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Step 3: Install Minikube:
download the latest Minikube binary:
```bash
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
Copy the downloaded file and store it into the /usr/local/bin/minikube directory :
```bash
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
```
give the file executive permission:
```bash
sudo chmod 755 /usr/local/bin/minikube
```
verify version of Minikube:
```bash
minikube version
```
Step 4: Install Kubectl:
Download kubectl:
```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```
Make the binary executable:
```bash
chmod +x ./kubectl
```
move the binary into path and Verify the installation :
```bash
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version -o json
```
Step 5: Start Minikube:
```bash
sudo minikube start --force --driver=docker
```
<p align="center">
<img src="images/Capture.PNG" alt="image" width="900" height="400">
</p>

enable  addons :
```bash
sudo minikube addons enable ingress
sudo minikube addons enable registry
sudo minikube addons enable metrics-server
```
<p align="center">
<img src="images/2.PNG" alt="image" width="900" height="400">
</p>

### Installation jenkins:
Step 1: Installing Java:
```bash
sudo apt update
sudo apt install openjdk-11-jdk
```
Step 2: Installing Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]  https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
```
The Jenkins service will launch automatically following installation:
<p align="center">
<img src="images/jenkinsstaus.PNG" alt="image" width="900" height="400">
</p>

### Containerizing my application :

Containerizing a Node.js application involves packaging the application along with its dependencies, libraries, and runtime environment into a container.

Step 1 : Create a Dockerfile in the root directory which  contains instructions for building the Docker image:

```bash
# Use an existing node image as base image
FROM node:14-alpine

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install required packages
RUN npm install

# Copy all files to the container
COPY . .

# Expose port 3000
EXPOSE 3000

# Start the application
CMD [ "npm", "start" ]
```
Step 2 : Build the Docker image :

<p align="center">
<img src="images/dockerbuild.PNG" alt="image" width="900" height="400">
</p>

## Contributing

Explain how others can contribute to your project. Include guidelines for submitting bug reports, feature requests, or code contributions. 

## License

Specify the license under which your project is distributed. Include any terms or conditions associated with the license.


