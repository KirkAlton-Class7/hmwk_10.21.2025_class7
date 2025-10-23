## Prerequisites and Skill Requirements

# Deploy Aaron’s VPC Demo
**Date:** 10-18-2025
<br>
**Class:** Class. 7 AWS
<br>
**Author:** [Kirk Alton](https://github.com/KirkAlton-Class7)

---
### Prerequisite 1: **Repo Setup**
Before starting, make sure you have access to one of the class Terraform repositories.  
#### Option 1: [Fork Theo's repo](https://github.com/malgus-waf/class5) or clone it locally.

```bash
git clone https://github.com/malgus-waf/class5.git
```

#### Option  2: [Fork the fork of Theo's repo](https://github.com/chewbaccawaf/class7) or clone it locally

```bash
git clone https://github.com/chewbaccawaf/class7
```

Both repositories have the Terraform files you'll need to complete the in class labs.

### Prerequisite 2: Required Software and Setup
Make sure the following are installed and configured:
- AWS CLI: check with `aws --version`
- Terraform: check with `terraform -version`
- VS Code: check with `code --version`
- Git: check with `git --version`

#### **Validate Prerequisite Installs**
Run Aaron’s script to check required software:

```bash
curl https://raw.githubusercontent.com/aaron-dm-mcdonald/Class7-notes/refs/heads/main/101825/check.sh | bash
```

> If you encounter errors, review the Aaron's notes here: [Class 7 Prerequisite README](https://github.com/KirkAlton-Class7/aaron_notes_class7/blob/main/101825/README.md#prereqs)

#### **Verify AWS CLI Authentication**
Run this in your terminal:

```bash
aws sts get-caller-identity
```

It should return the following:
- Your AWS user ID
- Account number
- ARN (Amazon Resource Name)

> If this command fails, verify your AWS credentials configuration in CLI or contact your group leader for help. You can also refer to the Class 7 Installation Document for additional information.

#### **Project Directory**

Make sure you have the following structure on your local machine:

```
~/Documents/TheoWAF/class7/AWS/Terraform/
```

### Prerequisite 3: Required Skills

#### P3.1: Basic Terminal Commands
Review the [Killer Code Linux Fundamentals](https://killercoda.com/pawelpiwosz/course/linuxFundamentals). You can also refer to a  [terminal cheat sheet](https://terminalcheatsheet.com/) for basic commands and navigation.

#### P3.2: Git and GitHub Basics
You should understand these basic Git commands and be comfortable performing them in terminal:
- `git init`

- `git status`

- `git add .`

- `git commit -m "Initial commit"`

- `git remote add origin <repo-URL>`

- `git push -u origin main`

- `git pull`

- `git clone <repo-URL>`

- `git branch git branch -M main`

<br>
<br>

[Git Cheat Sheet](https://git-scm.com/cheat-sheet)
<br>
#### P3.3: AWS Networking Fundamentals**
You should be familiar with VPC components and understand how to create and manage them in AWS.

> Tip: Review the AWS CLI commands for each concept to deepen your understanding and get familiar executing them in command line. You'll need knowledge of these commands when using Terraform.

- **VPC**
	- `aws ec2 create-vpc --cidr-block 10.0.0.0/16`
- **Subnet**
	- `aws ec2 create-subnet --vpc-id vpc-xxxxxxxx --cidr-block 10.0.1.0/24 --availability-zone us-east-1a`
- **Route Table**
	-  `aws ec2 create-route-table --vpc-id vpc-xxxxxxxx`
	- `aws ec2 associate-route-table --subnet-id subnet-xxxxxxxx --route-table-id rtb-xxxxxxxx`
- **Elastic IP**
	- `aws ec2 allocate-address --domain vpc`
- **Internet Gateway**
	- `aws ec2 create-internet-gateway`
	- `aws ec2 attach-internet-gateway --internet-gateway-id igw-xxxxxxxx --vpc-id vpc-xxxxxxxx`
- **NAT Gateway**
	- `aws ec2 create-nat-gateway --subnet-id subnet-xxxxxxxx --allocation-id eipalloc-xxxxxxxx`
- **VPC Endpoint**
- **Gateway Endpoint**

>Tip: Use `aws ec2 describe-RESOURCE` to show details about AWS resources you created (VPCs, subnets, rout tables, etc)

For a list of all AWS commands, refer to the [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/reference/).

### Prerequisite 4: Terraform Knowledge
#### P4.1: Terraform Syntax
Terraform code is made up of the following elements:
- **Blocks:** Containers that define objects such as resources. They can include arguments and nested blocks. Most Terraform configurations are made up of top-level blocks.
- **Arguments:** Assign values to names inside a block.
- **Expressions:** Represent values directly or by referencing and combining other values. Used as argument values or inside other expressions.
<br>
<br>[Terraform Syntax](https://developer.hashicorp.com/terraform/language)

#### P4.1: Terraform Terminology
Terraform uses HCL (HashiCorp Configuration Language) to define infrastructure. Make sure you understand these important concepts:
- [Provider](https://developer.hashicorp.com/terraform/language/block/provider): A plugin that enables Terraform to manage external services (e.g., AWS, GCP).
	- [AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Variable](https://developer.hashicorp.com/terraform/language/block/variable): A placeholder for input values that are used throughout Terraform configurations.
- [Resource](https://developer.hashicorp.com/terraform/language/block/resource): A block that defines a specific piece of infrastructure for Terraform to create, manage, or destroy.
- [Data](https://developer.hashicorp.com/terraform/language/block/data): A block that allows Terraform to read and retrieve information about existing infrastructure or external data managed outside of Terraform.
- [Terraform State File](https://developer.hashicorp.com/terraform/language/state): Stores metadata about managed resources and tracks their current state.
- [Indempotency](https://www.computerlanguage.com/results.php?definition=indempotency): The ability to run an operation multiple times and produce the same result, without creating unintended changes or side effects.
- [Execution Plan](https://developer.hashicorp.com/terraform/cli/commands/plan): Preview of what Terraform will create, modify or destroy.
- [Resource Drift / State Drift](https://developer.hashicorp.com/terraform/tutorials/state/resource-drift): Occurs when there are differences between your state file and real infrastructure.
#### P4.2: Basic Terraform Commands
Make sure you understand these basic commands:

| Command              | Purpose                                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `terraform init`     | Initializes the working directory and installs providers so Terraform commands can function correctly.                       |
| `terraform validate` | Checks the code for syntax and configuration errors.                                                                         |
| `terraform plan`     | Performs a dry run and shows the changes terraform will make before you apply them.                                          |
| `terraform apply`    | Executes changes that create, update or destroy resources according to your plan. Also updates the `terraform.tfstate` file. |
| `terraform destroy`  | Removes all managed infrastructure.                                                                                          |
| `terraform -help`    | Displays all available commands and options.                                                                                 |
[Terraform Cheat Sheet](https://cheat-sheets.nth-root.nl/terraform-cheat-sheet.pdf)

#### P4.3: Typical Terraform Workflow
1. Create or modify `.tf` files

2. Run `terraform init` to initialize the working directory.

3. Run `terraform validate` to check syntax

4. Run `terraform plan` to preview infrastructure changes

5. Review the plan carefully before applying changes

6. Run `terraform apply` to execute the plan

7. Terraform automatically updates the `terraform.tfstate` file
8. Run `terraform destroy` to remove all infrastructure when it's no longer needed.

<br>
[Aaron's Notes](https://github.com/aaron-dm-mcdonald/Class7-notes/blob/main/101825/README.md)
