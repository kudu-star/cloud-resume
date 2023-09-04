# cloud-resume
```
Project Scope

Overview
The cloud-resume project aims to create a basic website that includes a visitor counter. 
The counter will be implemented using a database and will update in real-time. 
The website will be hosted in the cloud and built using a CI/CD pipeline. 
The infrastructure will be defined using Infrastructure as Code and 
The website will be built using a serverless architecture.

Goals
- Create a basic website that includes a visitor counter
- Implement the visitor counter using a database
- Ensure the visitor counter updates in real-time
- Host the website in the cloud
- Build the website using a CI/CD pipeline
- Define the infrastructure using Infrastructure as Code
- Build the website using a serverless architecture

Deliverables
- A fully functional website that includes a visitor counter
- A database that stores the visitor count and updates in real-time
- A cloud-hosted website that is accessible to users
- A CI/CD pipeline that automatically builds and deploys the website
- Infrastructure as Code that defines the website's architecture
- A serverless architecture that minimizes costs and maximizes scalability

Timeline
This is a personal of mine and as I am doing this during my free time, I do not have a set timeline. 
I will be working on this project as I have time and will update this section as I progress.

Budget
Hosting costs: $50/month
Domain name: $10/year

Technologies
This project will use the following technologies:
Azure
Azure DevOps
Azure Functions
Azure Storage
Azure SQL cloud database
Azure Pipelines
Azure Resource Manager
Azure CLI
Terraform

# This project can be broken up in to the following stages:
1. Create a basic website
2. Create a visitor counter
3. Create a database
4. Create a CI/CD pipeline
5. Create a serverless architecture
6. Create a Infrastructure as Code
7. Write a blog post about the project

We're going to break up the "visitor counter"stage of the project - which requires creating a
cloud-based API that communicates with the website. 

We use an API that accepts a request from the website, increments the counter, and returns the
current count.

An Azure function with a web trigger is a good choice for this API, 
as it's serverless, can be scaled and is relatively cheap.

For the Azure function I will use some Python.
There will also be a test for the python code.

When all the above is working we can use IAC to deploy the function and database to Azure.

Using source control so that I don't have to update the API from my local machine
I'll be using CI/CD that connects to my Github repo

CI/CD backend will use Github Actions to build and deploy the function and database to Azure.
CI/CD frontend  will use a secondary Github Actions workflow to build and deploy the website to Azure.

Security note: Do not commit Azure credentials to source control.


**Next step:**

**Stage 1 - Create a basic website**