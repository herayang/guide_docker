## I. Installation

### Tools
- Docker: https://docs.docker.com/get-docker/
- VSCode: https://code.visualstudio.com/download
- Docker Extension: https://code.visualstudio.com/docs/containers/overview

### Troubleshooting
- https://github.com/docker/docker.github.io/issues
- https://github.com/microsoft/vscode/issues
- Troubleshooting tips for Docker: https://www.youtube.com/watch?v=E5ezkYSiNiE

## 1. Introduction - Josh Phillips

### 1.1 Docker Setup

- 
-
-
-

### 1.2 What is a Docker Image?

-
-
-

### 1.3 What is a Docker Container?

-
-
-

## 2. Creating the Docker File - Spencer Williams

### 2.1 What is a docker file?

![Docker File](https://user-images.githubusercontent.com/59627216/159536551-599e8e2a-f4e5-4a3d-8d49-42ede1d9a365.png)


- A text file with instructions for creating your docker image, which is a file with executable code. It is similar to a makefile for other programming languages and  their compliers but is used for the file to work with docker. 
- This in turn provides a form of automation for creating the docker image when creating for the first time and afterwards.
- A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.

### 2.2 Creating a docker file

- Via VS code extension, ... F1 while using the docker extension and selecting the type of file we want and its entry point (the main file it will execute)
- Via command line, touch DockerFile and vim Dockerfile to then edit it 
- docker list to view created docker files

### 2.3 Editing the docker file

FROM python:3.7 #
WORKDIR /app # Path to the image file
COPY requirements.txt ./requirements.txt # Copying our requirements.txt
RUN pip install -r requirements.txt # Runing it to install the necessary dependencies for your application to run
EXPOSE 8501 # The EXPOSE instruction tells Docker to get all its information required during the runtime from a specified Port. These ports can be either TCP or UDP, but it's TCP by default.
COPY . /app # Copy everything under the directory
ENTRYPOINT ["streamlit", "run"] # Setting the entry point
CMD ["main.py"] # Run file from the command line

## 3. Docker Build - Hera Yang

### 3.1

-
-
-

### 3.2

-
-
-

### 3.3

-
-
-

## 4. Running the Container - Mireya Vera Loo

### 4.1

-
-
-

### 4.2

-
-
-

### 4.3

-
-
-

## 5. Pushing to the Docker Hub - Ben Hinchman 

### 5.1

-
-
-

### 5.2

-
-
-

### 5.3

-
-
-

## 6. Docker Application - Caden Franc

### 6.1

-
-
-

### 6.2

-
-
-

### 6.3

-
-
-

## Additional Resources

- Docker Volumnes: https://docs.docker.com/storage/volumes/
- Docker Networks: https://docs.docker.com/network/
- Container Registries: https://docs.docker.com/registry/
- Docker Compose: https://docs.docker.com/compose/: 
- Docker vs. Kubernetes: https://semaphoreci.com/blog/kubernetes-vs-docker

## Other Resources
- [Docker Containers and Azure](https://github.com/BYUI451/cloud_guide/blob/main/azure.md) 
- [Using Spark for exploratory data analysis](https://github.com/BYUI451/spark_guide)
- [Docker](https://github.com/BYUI451/docker_guide)
- [Rocker Guide](https://github.com/BYUI451/rocker_guide)

