# Packer AMI Builder

This project utilizes HashiCorp Packer to create an Amazon Machine Image (AMI) with a predefined set of tools and configurations. The resulting AMI is designed to be a base image for your Amazon EC2 instances.

## Overview

This project leverages HashiCorp Packer to automate the creation of Amazon Machine Images (AMIs) in AWS. The primary goal is to streamline the process of provisioning EC2 instances with a pre-configured environment, including essential tools and dependencies.

Packer Configuration (aws-ami-v1.pkr.hcl)
The Packer configuration file defines the blueprint for creating the AMI. It specifies the base Amazon Machine Image, region, instance type, and a series of provisioners responsible for installing and configuring additional components.

Build Process
Base Image: The project starts with a base Amazon Linux image available in the specified region.

Provisioning: The provisioner script (provisioner.sh) is executed, updating the system packages, installing Git, AWS Systems Manager (SSM), CloudWatch agent, AWS Inspector, and Docker. It ensures that the resulting AMI is equipped with the necessary tools for development and monitoring.

CloudWatch Agent: The CloudWatch agent is configured to collect and report metrics from the EC2 instance.

AWS Inspector: AWS Inspector is installed to enhance security by identifying and addressing potential vulnerabilities.

Docker: The Docker engine is installed to enable containerized application deployment.

Provisioner Script (provisioner.sh)
The provisioner script is responsible for executing the necessary commands and installations during the provisioning phase. It performs the following tasks:

Updates system packages.
Installs Git, SSM, CloudWatch agent, AWS Inspector, and Docker.
Starts the CloudWatch agent and Docker daemon.
Jenkins Pipeline
The Jenkins pipeline automates the entire build process using the specified Docker image (hashicorp/packer:latest). It mounts the Docker socket to enable communication with the host's Docker daemon. The pipeline consists of a single stage, "Building AMI," where Packer initializes and builds the AMI based on the defined configuration.


## Prerequisites

Before using this Packer project, ensure you have the following prerequisites:

- [HashiCorp Packer](https://www.packer.io/downloads)
- AWS account credentials configured


