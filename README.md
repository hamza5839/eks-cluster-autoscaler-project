# EKS Cluster Autoscaler & Load Balancer Stress Test

## Project Summary
This project demonstrates a production-grade AWS EKS scaling solution. It automates the provisioning of EC2 worker nodes using the Kubernetes Cluster Autoscaler and exposes the application to the internet via an AWS Load Balancer.

## Key Accomplishments
* **Fixed RBAC Permissions:** Resolved `403 Forbidden` errors by patching the ClusterRole to allow `configmaps` access.
* **AWS Integration:** Configured OIDC identity federation for secure pod-to-AWS communication.
* **Stress Tested:** Successfully scaled from 1 node to 3 nodes in under 60 seconds by deploying 20 high-resource Nginx pods.

## How it Works
1. **Detection:** The Autoscaler identifies "Pending" pods that cannot fit on current nodes.
2. **Provisioning:** It updates the AWS Auto Scaling Group (ASG) Desired Capacity.
3. **Deployment:** AWS spins up new nodes; Kubernetes automatically schedules the pods onto them.
