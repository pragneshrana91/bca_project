
## Mail ID ranapragneshkumarkishorbhai@amityonline.com
## Enrollment No. : A9922523000450(el) Cloud and Security

## Pragnesh Rana 

## DevOps Project for Amity University BCA Last year project  
DevOps project for BCA last sam

--- **Terraform** ---
- Terraform is an open-source Infrastructure as Code (IaC) tool that enables defining and provisioning infrastructure declaratively using configuration files written in HashiCorp Configuration Language (HCL).
- It automates infrastructure deployment by communicating with cloud provider APIs to create, update, or remove resources as specified in the defined configuration, enabling consistent and repeatable environment setups.
- Terraform stores the state of the infrastructure, enabling tracking changes over time and planning infrastructure modifications before applying them.
- It supports multiple cloud providers like AWS, Azure, and Google Cloud, allowing unified management of hybrid or multi-cloud infrastructures.
- In our case for BCA_Last same project we are using terraform for AWS.

#There are two ways in which we can create and manage our infrastructure:
  -Manually approch.
Involves manually provisioning and configuring servers, networks, and resources through cloud provider consoles or CLI tools.
Error-prone, time-consuming, and difficult to maintain or scale, especially for complex environments.
  -Through automation.
Infrastructure is defined as code, making environments reproducible, auditable, and easy to maintain.
Automates provisioning and configuration, drastically reducing human errors and deployment time.
Facilitates collaboration through version-controlled infrastructure definitions.
Enables scaling and rapid environment spin-up/spin-down based on demand.


# Added AWS Access key ID and Secret access key to autheticate terraform to AWS.
# The aws_instance resource supports lifecycle management: creation, modification, and deletion of EC2 instances via Terraform commands (terraform apply, terraform destroy).
The very first step for initializing a Terraform project is to run the command:
1. terraform init - This command should be executed in the directory containing your Terraform configuration files (typically .tf files). It initializes the working directory, downloads the necessary provider plugins, configures the backend for storing state, and prepares modules needed for subsequent Terraform operations.
2. terraform plan - The terraform plan command is used to create an execution plan that previews the changes Terraform will make to your infrastructure based on your current configuration files.
3. terraform apply - The terraform apply command is used to execute the changes defined in your Terraform configuration files and make your cloud infrastructure match the desired state.
4. terraform destroy - The terraform destroy command is used to remove all infrastructure resources that have been provisioned and are currently managed by your Terraform configuration.

#Created bca_project_main.tf under the Terraform directory. This configuration automates the provisioning of AWS resources with a single command, eliminating the need for manual, interactive steps. By using Infrastructure as Code (IaC), this approach ensures consistency, repeatability, and reduces human errors in resource creation.

The Terraform code manages key AWS components including EC2 instances, security groups, and key pairs, all defined declaratively.

Sensitive data such as AWS access keys are handled securely via AWS CLI configuration rather than hard-coded in files.

Changes to the infrastructure can be tracked, versioned, and reviewed via source control to improve collaboration.

Terraform manages lifecycle states of resources to enable efficient updates, scaling, and teardown.

This method accelerates deployment workflows and enhances operational efficiency in cloud infrastructure management.

