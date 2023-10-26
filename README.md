[![CircleCI](https://dl.circleci.com/status-badge/img/gh/kerai2/Udacity-Project-4-Kubernetes/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/kerai2/Udacity-Project-4-Kubernetes/tree/main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

# Final Implementation

## Setup the Environment

### Create an AWS Cloud9 IDE
1. Create a AWS Cloud9 environment with m5 image (minimum requirements 2 vcpu and 4gb ram).

2. Install/verify [Docker](https://docs.docker.com/desktop/install/linux-install/)

3. Install [Hadolint](https://github.com/hadolint/hadolint)

4. Install/verify [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

5. Install [Minikube](https://minikube.sigs.k8s.io/docs/start/)

6. Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
    ```bash
    python3 -m pip install --user virtualenv
    # You should have Python 3.7 available in your host. 
    # Check the Python path using `which python3`
    # Use a command similar to this one:
    python3.7 -m venv .devops
    source .devops/bin/activate
    ```
7. Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  

    1. Run `python app.py`

2. Run in Docker:  

    1. Run `./run_docker.sh` to containerize the application to docker container (see script for steps).
    2. Run `./make_prediction.sh` to test the predict API on local.

3. Run in Kubernetes:  `./run_kubernetes.sh`

    1. Run `./upload_docker.sh` to push the docker image into docker hub (see script for steps).
    2. Run `minikube start` to start the local kubernetes cluster
    3. Run `kubectl config view` to view the kubernetes default configurations and verify that the cluster is with a certificate-authority and server.
    4. Run `./run_kubernetes.sh` to create and deploy flask app in container. Port forwarding fails due to pod still being setup. Wait 1 to 2 minutes
    5. Run `./run_kubernetes.sh` and verify port forwarding. When the pod is in [Running] state you
    6. Run `./make_prediction.sh` while calling `./run_kubernetes.sh`

4. Clean up local kubernetes cluster
    1. Run `minikube stop`
    2. Run `minikube delete` 
