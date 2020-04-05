# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

### Running the application locally using Docker
You can run the application locally by running:
```bash
docker-compose -f docker-compose-build.yaml build
docker-compose up
```

### Deploying Docker images to DockerHub
Deploying the Docker images can be easily achieved my performing `cd` into each directory, then build each image separately using `docker build -t NAME_OF_IMAGE .` and finally push each image to public DockerHub using `docker push NAME_OF_IMAGE:TAG`. If you haven't logged into Docker before pushing the images, you will need to run `docker login` and provide your Docker credentials. To pull the published Docker image of this project open a terminal and execute:
```bash
docker pull georgiosgoniotakis/udacity-c3-deployment
docker pull georgiosgoniotakis/udacity-c3-frontend
docker pull georgiosgoniotakis/udacity-c3-restapi-feed
docker pull georgiosgoniotakis/udacity-c3-restapi-user
```

### Deploying the application to a Kubernetes Cluster
There are many ways to use a Kubernetes cluster. My preferred way was to use minikube which allows you to deploy a miniature Kubernetes cluster on your local machine. After building the Docker image for each component locally, I triggered four deployments:
```bash
kubectl create deployment udacity-c3-frontend --image=georgiosgoniotakis/udacity-c3-frontend:latest
kubectl create deployment udacity-c3-restapi-user --image=georgiosgoniotakis/udacity-c3-restapi-user:latest
kubectl create deployment udacity-c3-restapi-feed --image=georgiosgoniotakis/udacity-c3-restapi-feed:latest
kubectl create deployment udacity-c3-deployment --image=georgiosgoniotakis/udacity-c3-deployment:latest
```
OR
```bash
kubectl apply -f <service-file-names>
kubectl apply -f <deployment-file-names>
```

<!-- ## Getting Setup

> _tip_: this frontend is designed to work with the RestAPI backends). It is recommended you stand up the backend first, test using Postman, and then the frontend should integrate.

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```
>_tip_: **npm i** is shorthand for **npm install**

### Setup Backend Node Environment
You'll need to create a new node server. Open a new terminal within the project directory and run:
1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript  @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`


### Configure The Backend Endpoint
Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```
*** -->