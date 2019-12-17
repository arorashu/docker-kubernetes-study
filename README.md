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


## Installation Results
 - There is no straight forward way to install Docker on Windows 10 Home
 - Docker does not work natively on WSL (Windows Subsystem for Linux) as well 
 - Cannot install on SCC, as no install permissions (also not available as a module, or brewfile)
 - Installed Docker on MacOS

## Memory Usage Comparison
 - Without docker: 195 MB
 - With Docker: 
  - Unique app size: 360 MB 
  - Shared size: 934 MB
  - Total size: 1.29 GB

## References

Install docker: https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly
Dockerize a React App: https://mherman.org/blog/dockerizing-a-react-app/
Docker Basics: https://docker-curriculum.com/

