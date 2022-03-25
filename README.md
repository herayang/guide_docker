## I. Installation

![Docker + VSCode](https://user-images.githubusercontent.com/59627216/159537585-d0b008e7-e9c6-4faf-9700-26fd5642f491.png)


### Tools
- Docker: https://docs.docker.com/get-docker/
- VSCode: https://code.visualstudio.com/download
- Docker Extension: https://code.visualstudio.com/docs/containers/overview

### Troubleshooting
- https://github.com/docker/docker.github.io/issues
- https://github.com/microsoft/vscode/issues
- https://www.youtube.com/watch?v=E5ezkYSiNiE

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

![Creating file](https://user-images.githubusercontent.com/59627216/159536991-19afc878-0b4e-43cd-9df4-f25f1b17aaf1.gif)


- Via VS code extension, ... F1 while using the docker extension and selecting the type of file we want and its entry point (the main file it will execute)
- Via command line, touch DockerFile and vim Dockerfile to then edit it 
- docker list to view created docker files

### 2.3 Editing the docker file

- *Selecting which python version to use (The FROM instruction initializes a new build stage and sets the Base Image for subsequent instructions)*
- FROM python:3.7
- *Path to the image file* 
- WORKDIR /app 
- *Copying our requirements.txt*
- COPY requirements.txt ./requirements.txt 
- *To install the necessary dependencies for your application to run*
- RUN pip install -r requirements.txt 
- *The EXPOSE instruction tells Docker to get all its information required during the runtime from a specified Port. These ports can be either TCP or UDP, but it's TCP by default.*
- EXPOSE 8501 
- *Copy everything under the directory*
- COPY . /app 
- *Setting the entry point or where your application will start*
- ENTRYPOINT ["streamlit", "run"] 
- *CMD allows you to input execute command lines when using your docker file (i.e. run main.py)*
- CMD ["main.py"] 

## 3. Docker Build - Hera Yang

### 3.1 Building an Image 

If Dockerfile is like a recipe, docker image is like a final product (eg. cake) of said recipe. Therefore, building the Dockerimage is the action of baking a cake(Dockerimage) following the given instruction(DockerFile.) Docker builds the image using the Dockerfile as the instruction and follows it step by step. Each instructions will create **a layer or an intermediate layer** that makes up the part of Dockerimage (the result of building Dockerfile) Keywords like `RUN`, `COPY`, or `ADD` will create a layer, while all other instructions will create an intermediate layer-- a layer that does not impact the size of the image created.

For our example Dockerfile, 

#### Caching
Each layers (including intermediate layers) are cached with a unique ID and can be shared and reused while building other images. For example, you have a docker file called A and another dockerfile called B, created based on Dockerfile A using `COPY`.  

![shared_layers](https://drive.google.com/uc?id=1D0IV41TKpDrASEkPVB43LcXuEtXlvlAd)

If we've already built file A and created an Dockerimage, the layers 1 and 2 is created, cached and ready to be reused. Therefore, when building Image B from Dockerfile B, Docker "skips" building the first two layer of Image B since it can reuse them. Therefore, these layers approaching for building an image helps Docker to be more efficient by eliminating any unnecessary, repetitive building. 


#### Order Matters
All layers are also dependant of the layers right below it since it is built on top of each other (kind of like a stack). This means that whenever a layer is modified, the changed layer and all the layers above it will have to be rebuilt. Therefore, keeping in mind the **heirarchy of the layers** could potentially impact the efficiency of the built image. 

![order](https://drive.google.com/uc?id=1UIQU-7v4B_7B7mAOu3Pv1HQ1a8Rdz8n7)

### 3.2 Command line build

You can build the image using the docker file created with the following command: 

```console
 $ docker build [OPTIONS] PATH | URL | -
```
- options: optional actions. 
  * `--tag`or `-t`:  The most common option you will see with build. Any images without a tag will, by default, have "latest" for its tag value. (*Always tagging your image is the best practice. *)
  *  `--cache-from`: sets image as part of build cache. Basically allowing the usual cache proceudre to work on different machines.
- PATH or URL : 
  * simply use `.` to build it in the current directory. 
  * URL refers to  Git repositories, pre-packaged tarball contexts and plain text files. Refer to documentation [here](https://docs.docker.com/engine/reference/commandline/build/)

#### 3.2.1 Commandline remove: 

Remove images by using the command below: 
```console
 $ docker rmi [OPTIONS] IMAGE [IMAGE...]
```
* note:  You cannot remove an image of a running container unless you use the `-f` option to force remove an image. Refer to the documentation [here](https://docs.docker.com/engine/reference/commandline/rmi/)


### 3.3 Further resources for understanding Images/Layers and its optimization.  

- [Optimization with Multi-stage Builds](https://docs.docker.com/develop/develop-images/multistage-build/)
- [Docker Layers Explained](https://dzone.com/articles/docker-layers-explained)
- [Docker Development Best Practice](https://docs.docker.com/develop/dev-best-practices/)
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

### 5.1 docker push [OPTIONS] NAME[:TAG]
- docker push behaves much like Github push does. It will push any changes made up to the image it is said to push to.
- for the [OPTIONS], you have -a, -q, and --disable-content-trust
- -a pushes all tagged images up to either your local repo or your cloud repo.
- NAME is the name of your image. [:TAG] is whatever tag you want to give it, like a version number.

### 5.2 docker push
- docker push MYIMAGE:VERSION // docker push myimage:1.0
- If you push myimage:1.0, make a change, and then make a new one, myimage:1.1, you will be able to grab both versions, and run the differences in them. Remember, each push is a unique, read-only image. Keeping track of Version History is helpful, much like Github Commits

### 5.3 Docker Hub
- docker login --username=yourhubusername --email=youremail@company.com
- After that, you'd be prompted to login. It'll save your password through the command line.
- docker tag [IMAGEID] [DOCKERUSERNAME]/[IMAGENAME]:[VERSION] //// docker tag myimage tujianis/image:1.5.5
- docker push [DOCKERUSERNAME]/[IMAGE] will //// docker push tujianis/centos
- docker pull [IMAGE] //// docker pull centos

## 6. Deployment to AWS - Caden Franc

- Learn how to create a free acount at https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/
- Login to your account and search the AWS Console for Elastic Beanstalk. This is a service provided by AWS for managing cloud applications.
- Create a new application and choose Docker as the platform.
- Under the "Source Code Origin" section, upload the [Dockerrun.aws.json](https://github.com/kstathou/vector_engine/blob/master/Dockerrun.aws.json) file. Be sure and change the image name to your own username and imagename.
- Choose the t2.micro instance if you are using the free tier. You will be charged for other options.




## Questions and Answers

- [Interview Questions for jobs that use Docker?](https://hackr.io/blog/docker-interview-questions)
- [What are the pros and cons of Docker?](https://blog.iron.io/docker-containers-the-pros-and-cons-of-docker/)
- [How to debug when using Docker in VSCode?](https://code.visualstudio.com/docs/containers/debug-common)
- [How to optimize Docker?](https://circleci.com/blog/tips-for-optimizing-docker-builds/)
- [How is Docker secure?](https://docs.docker.com/engine/security/#:~:text=Conclusions,or%20another%20appropriate%20hardening%20system.)

## Videos about and on using Docker

- [What is Docker in 5 mins](https://www.youtube.com/watch?v=_dfLOzuIg2o)
- [How to create and build Dockerfile](https://www.youtube.com/watch?v=LQjaJINkQXY)
- [Run Your App in a Container](https://www.youtube.com/watch?v=jtBVppyfDbE)

## Resources
- [Deploying Streamlit via Docker](https://www.section.io/engineering-education/how-to-deploy-streamlit-app-with-docker/)
- [Docker Containers](https://www.docker.com/resources/what-container/)
- [Docker Containers and Azure](https://github.com/BYUI451/cloud_guide/blob/main/azure.md) 
- [Using Spark for exploratory data analysis](https://github.com/BYUI451/spark_guide)
- [Docker](https://github.com/BYUI451/docker_guide)
- [Rocker Guide](https://github.com/BYUI451/rocker_guide)

## Additional Resources to Explore

- [Docker Volumes](https://docs.docker.com/storage/volumes/)
- [Docker Networks](https://docs.docker.com/network/)
- [Container Registries](https://docs.docker.com/registry/)
- [Docker Compose](https://docs.docker.com/compose/) 
- [Docker vs. Kubernetes](https://semaphoreci.com/blog/kubernetes-vs-docker)



