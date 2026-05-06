# Devop9
AWS Codebuild (Terraform to make EC2 instance and S3 bucket)
Here’s a **clean, copy-paste ready README-style version** of all the steps from your PDF, structured properly for GitHub 👇

---

# 🚀 Terraform AWS Setup (DevOps Experiment 9)

## 📌 Prerequisites

* Install Terraform CLI

### 1. Download Terraform

* Go to: [https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)
* Download **Windows 64-bit**

### 2. Install Terraform

* Extract `terraform.exe`
* Move it to a folder (example):

  ```
  C:\terraform
  ```

### 3. Add to PATH

* Search: `Edit system environment variables`
* Click **Environment Variables**
* Under **System Variables → Path → Edit → New**
* Add:

  ```
  C:\terraform
  ```

### 4. Verify Installation

```bash
terraform -version
```

---

## 🔐 Step 1: Create AWS IAM User

1. Go to AWS Console → IAM → Users
2. Click **Create User**
3. Enable **Programmatic access**
4. Attach permissions:

   * Select **Attach policies directly**
   * Choose:

     ```
     AdministratorAccess
     ```
5. Create user
6. Download the `.csv` file containing:

   * Access Key ID
   * Secret Access Key

---

## ⚙️ Step 2: Configure AWS Credentials

Set credentials in command prompt:

```bash
set AWS_ACCESS_KEY_ID=your_access_key
set AWS_SECRET_ACCESS_KEY=your_secret_key
set AWS_DEFAULT_REGION=us-east-1
```

---

## 📁 Step 3: Create Terraform Configuration

1. Create a new folder

2. Inside it, create file:

   ```
   main.tf
   ```

3. Add this code:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

# S3 Bucket
resource "aws_s3_bucket" "my_tf_bucket" {
  bucket = "devops_exp9"

  tags = {
    Name        = "My Terraform Bucket"
    Environment = "Dev"
  }
}

# EC2 Instance
resource "aws_instance" "my_server" {
  ami           = "ami-0440d3b780d96b29d"
  instance_type = "t3.micro"

  tags = {
    Name = "Terraform-Server"
  }
}
```

---

## ▶️ Step 4: Run Terraform

### Phase A: Initialize

```bash
terraform init
```

### Phase B: Plan

```bash
terraform plan
```

### Phase C: Apply

```bash
terraform apply
```

* Type:

  ```
  yes
  ```

### ✅ Verify

* Go to AWS S3 Console
* Check bucket:

  ```
  devops_exp9
  ```

---

## 🔄 Step 5: Modify Infrastructure

Update `main.tf` to add another EC2 instance:

```hcl
# Second EC2 Instance
resource "aws_instance" "my_second_server" {
  ami           = "ami-0440d3b780d96b29d"
  instance_type = "t3.micro"

  tags = {
    Name = "Terraform-Server-2"
  }
}
```

### Apply changes:

```bash
terraform apply
```

✔ Terraform will:

* Keep existing resources
* Only create the new EC2 instance

---



* format this with badges + screenshots (to make your README look 🔥)
* or convert it into a **GitHub project repo structure with files**
