# 🚀 Terraform AWS EC2 Instance Deployment

This is my **first Terraform project**, where I’ve created and deployed an **AWS EC2 instance** directly from the **CLI** using Terraform.  
The project demonstrates how to write Terraform configuration files, initialize Terraform, and manage infrastructure as code (IaC).

---

## 📘 Project Overview

In this project, I used **Terraform** to automate the creation of an **EC2 instance** on AWS.  
The goal was to understand Terraform’s workflow, including initialization, plan, apply, and destroy commands, while following best practices for infrastructure management.

---

## ⚙️ Technologies Used

- **Terraform** — Infrastructure as Code (IaC) tool  
- **AWS** — Cloud provider for hosting the EC2 instance  
- **CLI** — Command Line Interface for executing Terraform commands  

---

## 📁 Project Structure

├── terra.tf # Main Terraform configuration file
├── README.md # Project documentation
└── images/ # Screenshots showing Terraform commands and output


---

## 🧩 Key Terraform Concepts Covered

- **Providers:** Configuring AWS as a provider.  
- **Resources:** Defining EC2 instance as a Terraform-managed resource.  
- **Initialization:** Running `terraform init` to set up the working directory.  
- **Planning & Applying:** Using `terraform plan` and `terraform apply` to deploy infrastructure.  
- **State Management:** Understanding and managing Terraform state files.

---

## 🖼️ Screenshots

Below are some screenshots showing the Terraform workflow and AWS resource creation:

### Terraform Initialization
<img width="1440" alt="Terraform Init" src="https://github.com/user-attachments/assets/1ae26e2a-d595-4c11-a8a0-8f2da98bc55a">

### Terraform Apply
<img width="1440" alt="Terraform Apply" src="https://github.com/user-attachments/assets/26ed8eea-acfa-4fa4-a9ef-acc98a829b29">

### AWS EC2 Instance Created
<img width="1440" alt="EC2 Created" src="https://github.com/user-attachments/assets/d2c0ef6a-af27-4d45-85c0-91ee98bda24a">

---

## ⚠️ Important Note: State File Management

> Never store your Terraform **state files (`.tfstate`)** locally or in version control systems like GitHub.

Instead, store them securely using:
- **S3 Bucket** — For storing state files remotely.  
- **DynamoDB** — For state locking and consistency.

✅ **Correct Order for Secure State Management:**
1. Create an **S3 bucket** for Terraform state storage.  
2. Configure **DynamoDB** for state locking.  
3. Update the backend configuration in your Terraform file to point to the S3 bucket and DynamoDB table.  

Example:
```hcl
terraform {
  backend "s3" {
    bucket         = "your-terraform-state-bucket"
    key            = "terraform/state/terra.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-lock-table"
    encrypt        = true
  }
}
