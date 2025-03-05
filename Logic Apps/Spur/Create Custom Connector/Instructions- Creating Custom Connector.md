## Creating a Spur Custom Connector for Azure Logic Apps
*Instructions in progress ( Last updated: March 5,2025)*  
  
As of February 2025, there is no Spur connector in Azure Logic Apps, so creating your own Spur custom connector will give you better functionality to create multiple Spur logic apps.

## Instructions

[Create Logic Apps Connector | Microsoft Learn](https://learn.microsoft.com/en-us/connectors/custom-connectors/create-logic-apps-connector)

### Create Custom Connector
1. In the Azure portal, on the Azure services menu, select Create a resource.
2. In the New dialog, enter 'logic apps custom connector' in the search box, and then select Logic Apps Custom Connector from the dropdown list.
3. In the Logic Apps Custom Connector dialog, select Create.
4. Enter the details for registering your connector as described in the following table, and then select Review + create.  

| Property | Description | Example Text |  
| --- | --- | --- |  
| `Subscription` | Azure subscription for the connector | Azure Subscription |  
| `Resource group` | Azure resource group for the connector | logic-apps-custom-connectors |  
| `Name` | Name of your custom connector | SpurCustomConnector |  
| `Location` | Same Azure region as your logic app | (AU) Australia East |  

5. In the Create Logic Apps Custom Connector dialog, review the details you've entered, and then select Create.

### Setup Custom Connector  
1. In the resouce you have created, select **Overview**
2. In the top bar, select **Edit**  
 *Optional*: To import using a Postman collection, see [Postman | MS Learn](https://learn.microsoft.com/en-us/connectors/custom-connectors/define-postman-collection) and
Sentinel/Logic Apps/Spur/spur.postman_collection.json
3. Under **General information**  
   i. *Upload a connector icon for Spur.*  
   ii. **Host**: 'api.spur.us'  
   iii. **Base URL**: '/v2/context/'  
4. At the bottom right, select **Security**.  
5. Select the drop down under Authentication type, and choose 'API Key'.
   i. **Parameter label:** 'API Key'  
   ii. **Paremeter name:** 'APIKey'  
   iii. **Parameter location:** 'Header'  
6. At the bottom right, select **Definition**. This page is where you create the actions that will be available in the Logic App. If you have imported the postman collection in Step 2, skip to step ????
7. Under **General**  
   i. **Summary:** 'Submit IP'  
   ii. Description: 'Retrieves an IP Context Object by IPv4 or IPv6 Address. An IP Context Object summarizes all available information about the queried IP Address.'  
   iii. Operation ID: 'SubmitIP'  
   iv. Visibility: 'none'  
8. Under **Request**, Select *'Import from sample'*.  
    i. **Verb:** 'POST
    ii. **URL:** 'https://spur.us/context/'
    iii. **Headers:** 'use JSON from Sentinel/Logic Apps/Spur/IP Context Object Example.json'  
