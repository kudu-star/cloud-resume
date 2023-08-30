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

This project can be broken up in to the following stages:
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

Stage 1 Step-by-step guide:
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
az account set -s 8c781f5c-b4c9-4184-9915-7bb3b64a885e    #dev
```

4. Create a resource group by running the following command:
```bash
az group create --name <resource group name> --location <location>
```
Example:
```bash
 az group create --name dev-rg-website --location northeurope

 To destroy the resource group run the following command:
```bash
az group delete --name <resource group name>
```
example:
```bash
az group delete --name dev-rg-website

5. Create a storage account by running the following command:
```bash
az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_LRS
```
Example:
```bash
az storage account create --name devsacloudresume --resource-group dev-rg-website --location northeurope --sku Standard_LRS

Once the storage account has been created the console should display the output file of the account with all account details, alternatively, you can view the storage account by running the following command:
```bash
az storage account list --resource-group <resource group name> --output table
```
Example:
```bash
az storage account list --resource-group dev-rg-website --output table

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

10. Setup a custom domain name and SSL certificate for your website if you have not already done so. 
    (I can recommend using Cloudflare for this)
    
11. You can follow this guide provided my Microsoft to map a custom domain name to your Azure Storage account:
    https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal

12. Get the host name of your storage endpoint by running the following command:
```bash
az storage account show --name <storage-account-name> --query "primaryEndpoints.web" --output tsv
```
Example:
```bash
az storage account show --name devsacloudresume --query "primaryEndpoints.web" --output tsv
https://devsacloudresume.z16.web.core.windows.net/

13. Copy the value of the Blob service endpoint or the Static website endpoint to a text file. 
    You will need this value later.

14. Remove the protocol identifier (For example: HTTPS) and the trailing slash from that string. 
    The following table contains examples.
    Type of endpoint	endpoint	                                       host name
    blob service	    https://mystorageaccount.blob.core.windows.net/    mystorageaccount.blob.core.windows.net
    static website	    https://mystorageaccount.z5.web.core.windows.net/  mystorageaccount.z5.web.core.windows.net

    Example:
    My static website endpoint would be: https://devsacloudresume.z16.web.core.windows.net/
    and so the hostname would: devsacloudresume.z16.web.core.windows.net

15. Create an intermediate CNAME record that maps your custom domain name to the host name of your storage endpoint. 
    For example, if your custom domain name is www.contoso.com and your host name is mystorageaccount.z5.web.core.windows.net, 
    create a CNAME record that maps www.contoso.com to mystorageaccount.z5.web.core.windows.net.
    
    For example: asverify.mystorageaccount.blob.core.windows.net.
    
    My example:
    asverify.devsacloudresume.z16.web.core.windows.net.

16. Pre-Register the custom domain name with Azure by running the following command:
```bash
az storage account update --name <storage-account-name> --custom-domain <host-name> --use-subdomain true
```
    Replace the <resource-group-name> placeholder with the name of the resource group.
    Replace the <storage-account-name> placeholder with the name of the storage account.
    Replace the <custom-domain-name> placeholder with the name of your custom domain, including the subdomain.
    
    For example, if your domain is contoso.com and your subdomain alias is www, enter www.contoso.com. If your subdomain is photos, enter photos.contoso.com.

Example:
```bash
az storage account update --name devsacloudresume --custom-domain devsacloudresume.azureedge.net --use-subdomain true

16. Create a CNAME record that maps your custom domain name to the host name of your storage endpoint. 
    For example, if your custom domain name is www.contoso.com and your host name is mystorageaccount.z5.web.core.windows.net, 
    create a CNAME record that maps www.contoso.com to mystorageaccount.z5.web.core.windows.net.
    
    For example: www.contoso.com. 3600 IN CNAME mystorageaccount.z5.web.core.windows.net.
    My example:
    www.kudustar.uk. 3600 IN CNAME devsacloudresume.z16.web.core.windows.net.

17. Verify that the CNAME record is set up correctly by running the following command:
```bash
nslookup <subdomain-alias> <host-name>
```
Example:
```bash
nslookup www devsacloudresume.z16.web.core.windows.net

Test the custom domain is mapped to your storage account by creating ablob in your storage account and then navigating to the blob using your custom domain name ina browser. For example, if your custom domain name is www.contoso.com, navigate to https://www.contoso.com/blob-name.

My example:
https://www.kudustar.uk/index.html

18. Now map your custom domain with https enabled by enabling CDN on your web front end
    You can enable Azure Content Delivery Network (CDN) to cache content from a static website that is hosted in an Azure storage account. You can use Azure CDN to configure the custom domain endpoint for your static website, provision custom TLS/SSL certificates, and configure custom rewrite rules. Configuring Azure CDN results in additional charges, but provides consistent low latencies to your website from anywhere in the world. Azure CDN also provides TLS encryption with your own certificate.

19. Create the CDN endpoint by running the following command:
```bash
az cdn profile create --name <profile-name> --resource-group <resource-group-name> --sku Standard_Microsoft
````
Example:
```bash
az cdn profile create --name devsacloudresume --resource-group dev-rg-website --sku Standard_Microsoft

20. Now enable CDN for your static website by running the following command:
```bash
az cdn endpoint create --name <endpoint-name> --origin <storage-account-name>.z5.web.core.windows.net --profile-name <profile-name> --resource-group <resource-group-name> --origin-host-header <storage-account-name>.z5.web.core.windows.net --enable-compression --enable-http2 --query "hostName" --output tsv
```
Example:
```bash
az cdn endpoint create --name devsacloudresume --origin devsacloudresume.z16.web.core.windows.net --profile-name devsacloudresume --resource-group dev-rg-website --origin-host-header devsacloudresume.z16.web.core.windows.net --enable-compression --query "hostName" --output tsv



22. Map the permanent subdomain to the CDN endpoint by creating a CNAME record that maps 
    <subdomain-alias>.<custom-domain-name> to the host name of the CDN endpoint. 
    
    For example, if your custom domain name is www.contoso.com and your CDN endpoint host name is contoso.azureedge.net, 
    create a CNAME record that maps www.contoso.com to contoso.azureedge.net.

    For example: www.contoso.com. 3600 IN CNAME contoso.azureedge.net.

    My example:
    www.kudustar.uk. 3600 IN CNAME devsacloudresume.azureedge.net.

23. Verify that the CNAME record is set up correctly by running the following command:
```bash
nslookup <subdomain-alias> <host-name>
```
Example:
```bash
nslookup cdnverify devsacloudresume.azureedge.net

24. Verify that the CDN endpoint is working by running the following command:
```bash
curl -I <cdn-endpoint-host-name>
```
Example:
```bash
curl -I devsacloudresume.azureedge.net

25.Now add your custom domain to your cdn endpoint by running the following command:
```bash
az cdn custom-domain create --endpoint-name <endpoint-name> --hostname <custom-domain-name> --name <custom-domain-name> --profile-name <profile-name> --resource-group <resource-group-name>
```
Example:
```bash
az cdn custom-domain create --endpoint-name devsacloudresume --hostname www.kudustar.uk --name www-kudustar-uk --profile-name devsacloudresume --resource-group dev-rg-website




