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
        docker build -t sample:dev .
        docker run -v ${PWD}:/app -v /app/node-modules-p 3001:3000 --rm sample:dev

3. The application should be running at 

    localhost:3001

4. This app is running in Docker!



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

## Screenshots

create docker container

![https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F99e29276-a8cb-4046-a211-e7802de04bbe%2FScreenshot_2019-12-16_at_1.46.33_PM.png?table=block&id=b1ba1481-c014-428b-b388-fd702920fe10&width=4120&cache=v2](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F99e29276-a8cb-4046-a211-e7802de04bbe%2FScreenshot_2019-12-16_at_1.46.33_PM.png?table=block&id=b1ba1481-c014-428b-b388-fd702920fe10&width=4120&cache=v2)

run docker container

![https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb58c12fb-43bb-4e11-a17c-224a771202ec%2FScreenshot_2019-12-16_at_1.45.56_PM.png?table=block&id=cf7f1232-a220-478f-9daf-5d2d04fc2b1a&width=4120&cache=v2](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb58c12fb-43bb-4e11-a17c-224a771202ec%2FScreenshot_2019-12-16_at_1.45.56_PM.png?table=block&id=cf7f1232-a220-478f-9daf-5d2d04fc2b1a&width=4120&cache=v2)


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

![https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F566d9686-c088-43fb-875c-1087874d4c9a%2FScreenshot_2019-12-16_at_2.14.26_PM.png?table=block&id=b9028436-309c-404f-88c1-42e1646c50ec&width=3470&cache=v2](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F566d9686-c088-43fb-875c-1087874d4c9a%2FScreenshot_2019-12-16_at_2.14.26_PM.png?table=block&id=b9028436-309c-404f-88c1-42e1646c50ec&width=3470&cache=v2)

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

