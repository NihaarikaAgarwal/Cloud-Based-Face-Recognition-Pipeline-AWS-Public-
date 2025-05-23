# Cloud-Based Face Recognition on AWS – Design Overview

This repository outlines the system design and architecture for a multi-stage, cloud-to-edge face recognition pipeline developed as part of **CSE 546: Cloud Computing** at Arizona State University.

> ⚠️ **Note:** Per academic policy, code and internal documentation for this project are not shared publicly. This repository only provides high-level descriptions of the project structure and system design.

---

## 🧠 Project Overview

The project consists of two phases:

- **Project 1 (IaaS):** Manual provisioning of EC2-based infrastructure to handle image uploads and face recognition.
- **Project 2 (PaaS + Edge):** Serverless and edge-computing integration using AWS Lambda, ECR, and IoT Greengrass.

---

## 📦 Project Structure

''
cloud-computing-face-recognition-design/
│
├── project-1-iaas/ [IaaS: Web + App Tier]
│ ├── part-1-simpledb-web-tier [Single EC2 with S3 + SimpleDB]
│ └── part-2-autoscaling-multitier [Multi-tier with SQS-based autoscaling]
│
├── project-2-paas-edge/ [PaaS + Edge: Lambda & Greengrass]
│ ├── part-1-lambda-ecr [Dockerized Lambda pipeline]
│ └── part-2-edge-greengrass [Edge detection via Greengrass Core]
└── README.md [This design overview]''
