# Create custom lineage in Azure Purview

Data Catalog lineage user guide (preview) - Azure Purview | Microsoft Docs

As I am writing this small blog, [Azure Purview supports few data processing systems](https://docs.microsoft.com/en-us/azure/purview/catalog-lineage-user-guide); however, in reality, data engineers might be using third-party tools or custom scripts for data processing. Azure Purview provides a way to include such missing lineage information. 

This section will walk through setting up custom lineage between two Azure Data Lake Gen 2 storage in Azure purview.

## Prerequisite

1. [Azure Purview Quickstart](https://docs.microsoft.com/en-us/azure/purview/create-catalog-portal)
2. [Azure AD application Quickstart](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) 
3. [Postman] (https://www.postman.com/)  


The next step is to assign a role to application identity in Azure Purview. Azure purview doesn't allow direct access to the service. Therefore, every API request should have an authorization token.  

![AD app role assignment](/images/Image1.jpg) 

## Steps

Copy file "Azure Purview API Request.postman_collection.json" from [API_requests](/API_requests/) and import it in Postman

1) Open "01 Get Token", set Tenant_ID, Client_Id, Client_secret, click Send

![Get Auth Token](/images/Image2.jpg) 

2) Copy GUID for both storages as shown in the below image

![Get GUIDs](/images/storage1GUID.jpg) 

3)Open "02 Create Lineage" in Postman, provide a token (got in step 1) in Auth, provide input and output GUIDs under inputs and outputs section of JSON in Body tab. Click Send.

![Create lineage API request](/images/PostmanResponseSuccess.jpg) 

4) On successful response, check the Azure portal under the lineage tab of source or destination connection. You will see the lineage like the below image

![Custom Lineage on Azure portal](/images/Custom_Lineage_Azure_Portal.jpg) 


Thanks for reading and trying it out. Happy learning!! Would you mind creating a PR if you have any questions/feedback? 