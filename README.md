\# Terraform Docker Infrastructure as Code



\## Task 3: Infrastructure as Code (IaC) with Terraform



\### Objective



Provision and manage a local Docker container using Terraform.



The project uses Terraform to:



\* Pull the Nginx Docker image.

\* Create an Nginx Docker container.

\* Map the container's port 80 to host port 8082.

\* Verify the deployed container through a web browser.



\---



\## Tools Used



\* Terraform v1.16.5

\* Docker v28.1.1

\* Docker Desktop

\* Nginx

\* PowerShell

\* Windows



\---



\## Project Structure



```text

terraform-docker/

├── main.tf

├── README.md

├── execution-logs.txt

├── .terraform.lock.hcl

└── .gitignore

```



The `.terraform/` directory and Terraform state files are excluded from Git using `.gitignore`.



\---



\## Terraform Configuration



The `main.tf` file defines the Docker provider, Nginx image, and Nginx container.



\### Resources



1\. Docker Nginx image

2\. Docker Nginx container



\### Port Mapping



```text

Host:      8082

Container: 80

```



The application can therefore be accessed at:



```text

http://localhost:8082

```



\---



\## Terraform Commands



\### 1. Initialize Terraform



```powershell

terraform init

```



Terraform downloads and initializes the Docker provider.



\### 2. Validate the configuration



```powershell

terraform validate

```



Expected result:



```text

Success! The configuration is valid.

```



\### 3. Create an execution plan



```powershell

terraform plan

```



Terraform displays the resources that will be created.



\### 4. Apply the infrastructure



```powershell

terraform apply

```



Enter:



```text

yes

```



Terraform creates the Docker container.



\---



\## Port Conflict Troubleshooting



During the first deployment attempt, host port `8080` was already in use.



The existing Docker containers were checked using:



```powershell

docker ps

```



Port usage was also verified using:



```powershell

netstat -ano | findstr :8080

```



Instead of stopping the existing Jenkins service, the Terraform configuration was updated to use host port `8082`.



Final mapping:



```text

localhost:8082 → Nginx container:80

```



\---



\## Verification



After successful deployment:



```powershell

docker ps

```



The Terraform-managed container appeared as:



```text

terraform-nginx

```



with the port mapping:



```text

0.0.0.0:8082->80/tcp

```



The deployment was then verified by opening:



```text

http://localhost:8082

```



The Nginx Welcome Page was displayed successfully.



\---



\## Result



The infrastructure was successfully provisioned using Terraform.



\### Final Status



```text

Terraform initialization: SUCCESS

Terraform validation:     SUCCESS

Terraform plan:            SUCCESS

Terraform apply:           SUCCESS

Docker container:          RUNNING

Nginx deployment:          SUCCESS

Browser verification:      SUCCESS

```



\---



\## Key Learning



This task demonstrates the basic Infrastructure as Code workflow:



```text

Terraform Configuration

&#x20;       ↓

terraform init

&#x20;       ↓

terraform validate

&#x20;       ↓

terraform plan

&#x20;       ↓

terraform apply

&#x20;       ↓

Docker Container

&#x20;       ↓

Nginx Application

&#x20;       ↓

Browser Verification

```



The project demonstrates how Terraform can be used to declaratively provision and manage Docker infrastructure.



