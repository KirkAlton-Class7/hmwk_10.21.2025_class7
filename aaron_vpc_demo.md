# Deploy Aaron’s VPC Demo
**Date:** 10-18-2025
<br>
**Class:** Class. 7 AWS

---
## **Purpose**
This lab demonstrates how to deploy and tear down a simple AWS VPC using Terraform. You'll clone a preconfigured Terraform project, initialize it, validate the configuration, plan and apply the deployment, then verify the results in Terraform and the AWS Console. After deployment, you’ll destroy the infrastructure and confirm its removal in Terraform and the AWS console.

---
## Prerequisites and Skill Requirements
- Completion of [Terraform Dry Run](./terraform_dry_run.md)
- [View additional prerequisites and skill requirements here.](./prerequisites.md)

---
## **Stage 1: Set Up the Project Folder**

### **Step 1.2: Clone Aaron’s VPC Demo Repository**

Clone the preconfigured VPC demo repository. This is a standalone version I created based on [Aaron’s original VPC lab notes.](https://github.com/aaron-dm-mcdonald/Class7-notes/tree/main/101425) It makes it easier to clone and run independently:

```bash
git clone https://github.com/KirkAlton-Class7/aaron_vpc_demo.git
```

Navigate into the cloned folder:

```bash
cd aaron_vpc_demo
```

This folder contains a preconfigured Terraform setup that deploys Aaron's basic AWS VPC.

![01 – Git Clone and CD](./images/01_git_clone_cd.png)

---

## **Stage 2: Initialize and Validate Terraform**

### **Step 2.1: Initialize Terraform**

Initialize the project and download provider plugins:

```bash
terraform init
```

![02 – Terraform Init](./images/02_terraform_init.png)
### **Step 2.2: Validate Configuration**

Check for syntax or configuration errors:

```bash
terraform validate
```

![03 – Terraform Validate](./images/03_terraform_validate.png)


---

## **Stage 3: Plan and Apply the Configuration**

### **Step 3.1: Generate the Execution Plan**

Preview the infrastructure Terraform will create:

```bash
terraform plan
```

Review the output carefully before applying changes.

![04 – Terraform Plan](./images/04_terraform_plan.png)

### **Step 3.2: Apply the Plan**

Deploy the VPC and related resources:

```bash
terraform apply
```

When prompted, type:

```
yes
```

![05 – Terraform Apply (Confirm)](./images/05_terraform_apply_confirm.png)

Terraform will create the infrastructure and generate a `terraform.tfstate` file.

![06 – Terraform Apply (Complete)](./images/06_terraform_apply_complete.png)

---

## **Stage 4: Verify the Deployment**

### **Step 4.1: Verify Resources in Terraform State**

List all resources Terraform has deployed:

```bash
terraform state list
```

![07 – Terraform State List 1](./images/07_terraform_state_list_1.png)

### **Step 4.2: Verify via AWS Console**

- Log in to the AWS Management Console.
- Navigate to **VPC → Your VPCs** and confirm the new VPC exists.
- Check subnets, route tables, and gateways as needed.

> The demo VPC deploys in the us-east-1 region. Make sure you select this region in the AWS console, otherwise the VPC will not appear in your list.


![08 – AWS Confirmation 1](./images/08_aws_confirmation_1.png)

![09 – AWS Confirmation 2](./images/09_aws_confirmation_2.png)

---

## **Stage 5: Destroy the Infrastructure**

### **Step 5.1: Tear Down the Resources**

Run the destroy command to remove all deployed resources:

```bash
terraform destroy
```

When prompted, type:

```
yes
```

![10 – Terraform Destroy (Confirm)](./images/10_terraform_destroy_confirm.png)

Terraform should give confirmation that the infrastructure was destroyed.

![11 – Terraform Destroy (Complete)](./images/11_terraform_destroy_complete.png)

### **Step 5.2: Confirm Deletion**

Verify all resources have been removed:

```bash
terraform state list
```

Should show no results (no output)

![12 – Terraform State List 2](./images/12_terraform_state_list_2.png)

### **Step 5.3: Double-Check in AWS Console**

Return to the AWS Management Console and confirm that:
- The VPC has been deleted.
- All associated resources subnets, gateways, route tables, and other resources are removed.

![13 – AWS Confirmation 2 (Post-Destroy)](./images/13_aws_confirmation_2.png)

---

## **Cleanup**
Remove the local demo folder if no longer needed:

```bash
cd ..
rm -rf aaron_vpc_demo
```
