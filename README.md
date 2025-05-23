# Cloud-Based Face Recognition on AWS – Design Overview

This repository outlines the system design and architecture for a multi-stage, cloud-to-edge face recognition pipeline developed as part of **CSE 546: Cloud Computing** at Arizona State University.

> **Note:** Per academic policy, code and internal documentation for this project are not shared publicly. This repository only provides high-level descriptions of the project structure and system design.

---

## Project Overview

The project consists of two phases:

- **Project 1 (IaaS):** Manual provisioning of EC2-based infrastructure to handle image uploads and face recognition.
- **Project 2 (PaaS + Edge):** Serverless and edge-computing integration using AWS Lambda, ECR, and IoT Greengrass.

---

## Project Structure


Descriptions:
- `project-1-iaas/`: IaaS: Web + App Tier
  - `part-1-simpledb-web-tier`: Single EC2 with S3 + SimpleDB
  - `part-2-autoscaling-multitier`: Multi-tier with SQS-based autoscaling
- `project-2-paas-edge/`: PaaS + Edge: Lambda & Greengrass
  - `part-1-lambda-ecr`: Dockerized Lambda pipeline
  - `part-2-edge-greengrass`: Edge detection via Greengrass Core

---

##  Project 1 – IaaS-Based Web and App Tiers

### Part 1: Web Tier with SimpleDB
**Path**: `project-1-iaas/part-1-simpledb-web-tier`

- A single EC2 instance runs a Python Flask server  
- Accepts image uploads and stores them in S3  
- Performs face identification using a mock lookup in SimpleDB  
- Designed for fixed-scale, single-tier deployments  

### Part 2: Multi-Tier with Autoscaling
**Path**: `project-1-iaas/part-2-autoscaling-multitier`

- Adds an autoscaled application tier using custom EC2 orchestration  
- Web tier pushes messages to an SQS request queue  
- App tier EC2s (launched from AMI) read from queue, perform inference, and push to response queue  
- `controller.py` handles horizontal scaling logic up to 15 instances  
- No use of AWS Auto Scaling groups — scaling done via Python scripts  

---

## Project 2 – PaaS and Edge Deployment

### Part 1: Serverless with Lambda + ECR
**Path**: `project-2-paas-edge/part-1-lambda-ecr`

- Pipeline decomposed into two Lambda functions: `face-detection` and `face-recognition`  
- Each Lambda is packaged in a Docker container and deployed via ECR  
- Communication handled via SQS queue between stages  
- Function URLs used for invocation testing  
- Tools: `facenet-pytorch`, `OpenCV`, `boto3`  

### Part 2: Edge Detection with IoT Greengrass
**Path**: `project-2-paas-edge/part-2-edge-greengrass`

- Face detection runs on an emulated IoT device using AWS Greengrass v2  
- EC2 device acts as the Greengrass core, running MTCNN as a component  
- A lightweight client simulates camera input and publishes images via MQTT  
- After detection, cropped faces are sent to the cloud for recognition using Lambda  
- Enables real-time edge-to-cloud inference with secure messaging  

---

## 📫 Want to Learn More?

I'm happy to discuss the system architecture, edge vs. cloud design trade-offs, and implementation lessons.

📧 **Contact**: [your.email@domain.com](mailto:your.email@domain.com)
