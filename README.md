# 🚀 AWS EKS Cluster with Autoscaling (Hands-on Project)

## 📌 Overview

This project demonstrates the complete setup of a production-style Kubernetes environment on AWS using **Amazon EKS**. It covers infrastructure creation, cluster configuration, node management, and autoscaling, followed by deploying a sample application to validate scaling behavior.

The setup is primarily performed using the **AWS Management Console**, with cluster interaction via `kubectl`.

---

## 🧱 Architecture Components

* VPC (created via CloudFormation)
* EKS Control Plane
* Managed Node Group (EC2 worker nodes)
* Cluster Autoscaler
* Sample Application (NGINX)
* Kubernetes Services (LoadBalancer)

---

## ⚙️ Implementation Steps

### 1️⃣ VPC Creation

* Created a VPC using AWS CloudFormation template
* Configured:

  * Public & private subnets
  * Internet Gateway
  * Route tables

---

### 2️⃣ EKS Cluster Setup

* Created EKS cluster via AWS Console
* Configured networking using created VPC
* Enabled public endpoint access

---

### 3️⃣ Cluster Access

* Connected locally using:

```bash
aws eks update-kubeconfig --name eks-cluster --region <region>
```

---

### 4️⃣ Node Group Configuration

* Created IAM role for worker nodes
* Attached required policies:

  * AmazonEKSWorkerNodePolicy
  * AmazonEKS_CNI_Policy
  * AmazonEC2ContainerRegistryReadOnly
* Created managed node group (EC2 instances)

---

### 5️⃣ Cluster Autoscaler Setup

#### IAM Configuration

* Created custom IAM policy with permissions:

  * autoscaling:Describe*
  * autoscaling:SetDesiredCapacity
  * autoscaling:TerminateInstanceInAutoScalingGroup
  * ec2:DescribeLaunchTemplateVersions

* Attached policy to Node Group IAM Role

#### Deployment

* Deployed Cluster Autoscaler to EKS cluster
* Configured with correct cluster name
* Verified pod status and logs

---

### 6️⃣ Application Deployment

#### NGINX Deployment

* Created Kubernetes Deployment with multiple replicas

#### Service Exposure

* Exposed application using:

```yaml
type: LoadBalancer
```

* Verified external access via AWS Load Balancer

---

### 7️⃣ Autoscaling Test

* Scaled application:

```bash
kubectl scale deployment nginx --replicas=20
```

### Observed Behavior:

* Pods entered **Pending** state
* Cluster Autoscaler detected resource shortage
* Node group scaled up automatically
* New EC2 instances launched
* Pods scheduled successfully

---

## 🧠 Key Learnings

* Understanding EKS architecture and components
* Difference between control plane and worker nodes
* Kubernetes service types (ClusterIP, NodePort, LoadBalancer)
* IAM roles and permissions for autoscaling
* Real-world debugging of:

  * LoadBalancer issues
  * Subnet tagging
  * DNS resolution
* How Cluster Autoscaler interacts with AWS Auto Scaling Groups

---

## 🛠️ Tools & Technologies

* AWS EKS
* AWS CloudFormation
* EC2 (Node Groups)
* Kubernetes (`kubectl`)
* IAM
* NGINX

---

## 📈 Future Improvements

* Implement Ingress Controller (ALB)
* Add Horizontal Pod Autoscaler (HPA)
* Use IAM Roles for Service Accounts (IRSA)
* Add monitoring (Prometheus + Grafana)
* CI/CD integration (GitHub Actions)

---

## 👨‍💻 Author

Muhammad Hamza gpt

---

## ⭐Learning  CREDITS goes TO Techworld nana <3

