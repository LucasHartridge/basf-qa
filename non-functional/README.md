# Non Functional Requirements

## How it works ?

Our load testing framework is based on [locust.io v1.4.0](https://docs.locust.io/en/stable/) that is used with Python 3

This framework is based in src/locust.py file. This file contains all the logic for the load testing. Right now is only set to verify that the response is 200, but you will see that there is a line commented that shows the response of the data (You can check the locustfile.log)

The logic is very simple, is just testing the GET person/all endpoint. You can see that there is a variable called wait_time. This variable will wait between 1 and 2 seconds before re starting the process, that is why you will need to have 600 users in order to achieve 300 RPS constantly. The idea behind this framework is to test how many concurrent users you can have on the application but also you can see Request Per Seconds (RPS) metrics and much more

## How to Set up Locust Locally

1. Install Python. Make sure you download the latest version of Python 3
2. Install Pip for Python 3
3. Install Virtualenv
   - `pip3 install virtualenv`
4. Create a virtualenv for the actual project
   - `virtualenv -p python3 <path/to/new/virtualenv/>`
5. Activate the virtual env in the loadTesting Project
   - `source <path/to/new/virtualenv>/bin/activate`
6. Install the pip packages needed by this project
   - `pip install -r </path/to/load/testing/project/>requirements.txt`
7. Run the locust tests locally

- No Web: `locust -f ./src/locust.py --logfile=./locustfile.log --loglevel=DEBUG --headless -u 600 -r 50 -t 60s -H http://azure-qknows-prod-challenges-1.northeurope.cloudapp.azure.com`
  - Parameters from No Web:
    - **-u**: Number of users generated by Locust
  - **-r**: Time in seconds untill a new user starts executing tasks (with a maximum of the number of users defined by -c) - Hatch rate of users. For example if you set 1, 1 user per second will be added until the maximum amount of users (c) is reached
    - **-t**: How long the Locust tests should be running
- Web: `locust -f ./src/locust.py --logfile=./locustfile.log -H http://azure-qknows-prod-challenges-1.northeurope.cloudapp.azure.com`
- Web Dev: `locust -f ./locust.py --logfile=./locustfile.log -H http://azure-qknows-prod-challenges-1.northeurope.cloudapp.azure.com`

  After this you will need to open your browser in localhost:8089 and enter the number of users to hatch for example 600 in order to perform 300 operations per second as it was requested in the inverview document.

  In order to stop the process you will need to kill the process in the terminal

**Note**: If you receive an error running the test that Locust is not found, open a new terminal and activate again the Virtual Env will it

## Docker Image

I have created a Dockerfile in order to make it easy for the person who will review this. Installing Python, pip sometimes can take time if you did not have installed it previously

1. Open a Terminal
2. Run `docker build -t lt-basf .`
3. Run `docker run -ti -p 8089:8089 -e "OPTS=--logfile=./locustfile.log --loglevel=DEBUG --headless -u 600 -r 50 -t 60s -H http://azure-qknows-prod-challenges-1.northeurope.cloudapp.azure.com" lt-basf`
