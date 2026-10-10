			AWS EC2, Docker, Load Balancer & Auto Scaling Project

Project Overview

This project demonstrates the deployment of a Flask web application on AWS EC2 using Docker, an Application Load Balancer (ALB), and an Auto Scaling Group (ASG).

The application displays information about the EC2 instance serving the request, including:

EC2 hostname

AWS Availability Zone

Application status

A /health endpoint is also provided for load balancer health checks.

Project Flow

Flask Application
       ↓
Docker Container
       ↓
EC2 Instances
       ↓
Target Group
       ↓
Application Load Balancer

Auto Scaling Group manages EC2 capacity

AWS Services Used

Amazon EC2

Amazon Machine Image (AMI)

EC2 Launch Template

Application Load Balancer

Target Group

Auto Scaling Group

Target Tracking Scaling Policy

Technologies Used

Ubuntu Linux

Python

Flask

Docker

Bash

AWS

Project Components

1. Flask Application

Developed a Flask web application that displays the EC2 hostname, Availability Zone, and application status.

The application also provides a health-check endpoint:

GET /health

Expected response:

OK

HTTP status code: 200

2. Docker

Created a Dockerfile for the Flask application.

Built a Docker image.

Ran the application inside a Docker container.

Configured the container to expose the application on the required port.

3. Amazon Machine Image (AMI)

Created an AMI from the configured EC2 instance to preserve the application environment for launching additional instances.

4. EC2 Launch Template

Created a Launch Template containing the required instance configuration, including:

AMI

Instance type

Security group

Key pair, where required

User Data script

The User Data script configures the instance and starts the Docker application during launch.

5. Target Group

Configured a Target Group to route requests to EC2 instances.

Health-check configuration:

Protocol: HTTP

Port: 80

Path: /health

The Target Group checks whether the application is responding correctly before routing traffic to a healthy target.

6. Application Load Balancer

Configured an internet-facing Application Load Balancer with an HTTP listener to forward incoming requests to the Target Group.

Request flow:

Client
  ↓
Application Load Balancer
  ↓
Target Group
  ↓
Healthy EC2 Instance
  ↓
Docker Container
  ↓
Flask Application

7. Auto Scaling Group

Configured an Auto Scaling Group to manage the EC2 instances used by the application.

Capacity configuration:

Minimum capacity: 1

Desired capacity: 1

Maximum capacity: 3

Configured a target tracking scaling policy based on average CPU utilization.

Two EC2 instances were observed running during project testing. This demonstrates that multiple instances were running, but automatic scale-out is considered verified only when the scaling policy is confirmed to have launched an additional instance.

Project Implementation Steps

Launched an Ubuntu EC2 instance and connected.

Created the Flask application.

Installed Docker.

Built a Docker image for the application.

Ran the Docker container and tested the application locally.

Created an AMI from the configured instance.

Created a Launch Template with the required configuration and User Data.

Created a Target Group with an HTTP health check on port 80 using /health.

Created an Application Load Balancer and configured its listener.

Created an Auto Scaling Group using the Launch Template.

Configured a CPU utilization-based target tracking policy.

Tested the application through the Load Balancer DNS name.

Observed EC2 instances and reviewed the Auto Scaling configuration.

Repository Structure

EC2-AutoScaling-LoadBalancer/
├── app.py
├── Dockerfile
├── requirements.txt
├── user-data.sh
├── README.md
└── screenshots/
    ├── flask-app-run.png
    ├── ami.png
    ├── template.png
    ├── ec2-instances-running.png
    ├── load-balancer.png
    ├── auto-scaling-group.png(ALL STEPS OF AUTO-SCALING)

Health Check

The application provides the following endpoint:

GET /health

Expected response: OK

Expected HTTP status code: 200

This endpoint is used by the Target Group to check application health.

Learning Outcomes

Through this project, I gained hands-on practice with:

EC2 instance management

Linux administration

Flask application deployment

Docker images and containers

AMI creation

Launch Templates and User Data

Target Groups and health checks

Application Load Balancers

Auto Scaling Groups

CPU-based target tracking policies

AWS infrastructure configuration

					Important Notes

Auto Scaling was configured with a CPU utilization-based target tracking policy.

Two running EC2 instances were observed during testing.

Automatic scale-out should only be claimed as successfully demonstrated if an additional instance was confirmed to have launched automatically because of the scaling policy.


