# Docker-study
Do a study of the docker technology, use on a simple application, and document results

## ECE-601 - Mini Project 3
This project is part of Mini Project 3 for Product Design Class at BU, Fall 2019.
Teammates: Shubham Arora & Krishna Chaitanya 

## Aim
We try to run the Spark Digital Equity WebApp: https://github.com/arorashu/spark-digital-equity.git
in docker. We will document the steps, compare app size, and deploy times.

## Introduction

### What is Docker?
Docker is an open-source project that automates the deployment of software applications inside containers by providing an additional layer of abstraction and automation of OS-level virtualization on Linux.


## How to Reproduce?

1. Ensure you have Docker installed
2. Run the following commands

        git clone [https://github.com/arorashu/spark-digital-equity](https://github.com/arorashu/spark-digital-equity)
        cd spark-digital-equity

3. Create file "dockerfile" with contents as given below:
        
        # base image
        FROM node:13.3.0
        
        # set working directory
        WORKDIR /app
        
        # add `/app/node_modules/.bin` to $PATH
        ENV PATH /app/node_modules/.bin:$PATH
        
        # install and cache app dependencies
        COPY package.json /app/package.json
        RUN npm install --silent
        RUN npm install react-scripts@3.0.1 -g --silent
        
        # start app
        CMD ["npm", "start"]

4. Create file ".dockerignore" with contents:

        node_modules


5. Run the following commands:

        docker build -t sample:dev .
        docker run -v ${PWD}:/app -v /app/node-modules-p 3001:3000 --rm sample:dev

6. The application should be running at 

        localhost:3001

7. This app is running in Docker!
8. Any changes you make to the app code will be hot reloaded!



## Installation Results
 - There is no straight forward way to install Docker on Windows 10 Home
 - Docker does not work natively on WSL (Windows Subsystem for Linux) as well 
 - Cannot install on SCC, as no install permissions (also not available as a module, or brewfile)
 - Installed Docker on MacOS


# Results

## Without Docker

Run application

    npm install
    npm start

## With Docker

    docker build -t sample:dev .
    docker run -v ${PWD}:/app -v /app/node-modules-p 3001:3000 --rm sample:dev

# Screenshots

## create docker container

![https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%201.46.33%20PM.png](https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%201.46.33%20PM.png)

run docker container

![https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%201.45.56%20PM.png](https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%201.45.56%20PM.png)


## Dockerfile

    # base image
    FROM node:13.3.0
    
    # set working directory
    WORKDIR /app
    
    # add `/app/node_modules/.bin` to $PATH
    ENV PATH /app/node_modules/.bin:$PATH
    
    # install and cache app dependencies
    COPY package.json /app/package.json
    RUN npm install --silent
    RUN npm install react-scripts@3.0.1 -g --silent
    
    # start app
    CMD ["npm", "start"]

## Memory Usage Comparison
 - Without docker: 195 MB
 - With Docker: 
   - Unique app size: 360 MB 
   - Shared size: 934 MB
   - Total size: 1.29 GB

## App size

![https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%202.14.26%20PM.png](https://github.com/arorashu/docker-study/blob/master/screenshots/Screenshot%202019-12-16%20at%202.14.26%20PM.png)

## Conclusion
 - Docker allows in containerization and reproducibility of a dev environment
 - It however adds memory size to the application
 - For very small or single applicaions, the extra memory usage may not be justified
 - The use case of docker shines however in case of microservices and composability of various stacks of an application( multiple databses, front-end , back-end ).
 - A more integrated analysis should be done with a complex application to analyze these use cases

## References

- Install docker: https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly
- Dockerize a React App: https://mherman.org/blog/dockerizing-a-react-app/
- Docker Basics: https://docker-curriculum.com/

## Time taken
Around 3 hours

