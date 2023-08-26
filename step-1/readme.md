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

This project can be broken up in to the following sections:
1. Create a basic website
2. Create a visitor counter
3. Create a database
4. Create a CI/CD pipeline
5. Create a serverless architecture
6. Create a Infrastructure as Code
7. Write a blog post about the project

Next steps:
1. Create a basic website
links:https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to?tabs=azure-cli#enable-static-website-hosting

Step 1 Step-by-step guide:
1. Login to your Azure account
2. Now view which subscriptions you have by running the following command:
```bash
az account list --output table
```
Example:
```bash
az account list --output table
A few accounts are skipped as they don't have 'Enabled' state. Use '--all' to display them.
Name    CloudName    SubscriptionId                        TenantId                              State    IsDefault
------  -----------  ------------------------------------  ------------------------------------  -------  -----------
dev     AzureCloud   8c781-------------------------------  9f0------------------------------  Enabled  True
prod    AzureCloud   2a5ed-------------------------------  9f0------------------------------  Enabled  False

3. Set the subscription you want to use by running the following command:
```bash
az account set --subscription <subscription name>
```
Example:
```bash
az account set --subscription Visual Studio Enterprise
```

4. Create a resource group by running the following command:
```bash
az group create --name <resource group name> --location <location>
```
Example:
```bash
 az group create --name dev-rg-website --location ukwest

 To destroy the resource group run the following command:
```bash
az group delete --name <resource group name>
```

5. Create a storage account by running the following command:
```bash
az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_LRS
```
Example:
```bash
az storage account create --name devsacloudresume --resource-group dev-rg-website --location ukwest --sku Standard_LRS

Once the storage account has been created the console should display the output file of the account with all account details, alternatively, you can view the storage account by running the following command:
```bash
az storage account list --resource-group <resource group name> --output table
```
To destroy the storage account run the following command:
```bash
az storage account delete --name <storage account name> --resource-group <resource group name>
```
6. Enable static website hosting (a feature you will need to enable on your storage account) 
    by running the following command:
```bash
az storage blob service-properties update --account-name <storage-account-name> --static-website --404-document <error-document-name> --index-document <index-document-name>
```
Replace <storage-account-name> with the name of your storage account.
Replace index.html with the name of the file you want to be the index page of your website.
Replace the error document with the name of the file you want to be the error page of your website.

Example:
```bash
az storage blob service-properties update --account-name devsacloudresume --static-website --404-document error.html --index-document index.html

7. Upload your files to the storage account by running the following command:
```bash
az storage blob upload-batch --account-name <storage-account-name> --source <source-folder> --destination <destination-folder>
```
Example:
```bash
az storage blob upload-batch --account-name devsacloudresume --source . --destination '$web'

8. View your site Url by running the following command:
```bash
az storage account show --name <storage-account-name> --query "primaryEndpoints.web" --output tsv
```
Example:
```bash
az storage account show --name devsacloudresume --query "primaryEndpoints.web" --output tsv

9. Optional: Enable metrics on the website.
