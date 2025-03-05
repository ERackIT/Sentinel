## Creating a Spur Custom Connector for Azure Logic Apps
*Last updated: March 5, 2025*  
  
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

### Setup Custom Connector from scratch
1. In the resouce you have created, select **Overview**
2. In the top bar, select **Edit**  
3. Under **General information**  
   i. *Upload a connector icon for Spur.*  
   ii. **Host**: 'api.spur.us'  
   iii. **Base URL**: '/v2/context/'  
4. At the bottom right, select **Security**.  
5. Select the drop down under Authentication type, and choose 'API Key'.
   i. **Parameter label:** 'API Key'  
   ii. **Paremeter name:** 'APIKey'  
   iii. **Parameter location:** 'Header'  
6. At the bottom right, select **Definition**. This page is where you create the actions that will be available in the Logic App.
7. Under **General**  
   i. **Summary:** 'GET IP Context'  
   ii. Description: 'Retrieves an IP Context Object by IPv4 or IPv6 Address. An IP Context Object summarizes all available information about the queried IP Address.'  
   iii. Operation ID: 'GetIPContext'  
   iv. Visibility: 'none'  
8. Under **Request**, Select *'Import from sample'*.  
    i. **Verb:** 'GET'
    ii. **URL:** 'https://api.spur.us/v2/context/'
    iii. **Headers:** 'Content-Type application/json'
9. Select **Import**
10. Under **Response**, Select *Add default response*.
    i. **Headers:** 'Content-Type application/json'
    ii. **Body:** *copy and paste .json from [IP Context Object Example.json](https://github.com/ERackIT/Sentinel/blob/main/Logic%20Apps/Spur/Create%20Custom%20Connector/IP%20Context%20Object%20Example.json)
11. Select **Import**
12. At the top of the page, select **Update Connector**.

### Setup Custom Connector using Postman 
1. Navigate to [Sentinel/Logic Apps/Spur/spur.postman_collection.json](https://github.com/ERackIT/Sentinel/blob/main/Logic%20Apps/Spur/Create%20Custom%20Connector/spur.postman_collection.json)
2. Copy json and paste in a Notepad file on your desktop.
3. Replace *{{API Key}}* with your API Key
4. Save file as *'spur.postman_collection.json'*
5. In the resouce you have created, select **Overview**
6. In the top bar, select **Edit**  
7. In the resouce you have created, select **Overview**
8. In the top bar, select **Edit**
9. Under **General information**  
   i. *Upload a connector icon for Spur.*  
   ii. **Host**: 'api.spur.us'  
   iii. **Base URL**: '/v2/context/'  
10. At the bottom right, select **Security**.  
11. Select the drop down under Authentication type, and choose 'API Key'.
   i. **Parameter label:** 'API Key'  
   ii. **Paremeter name:** 'APIKey'  
   iii. **Parameter location:** 'Header'  
12. At the bottom right, select **Definition**.
13. Under **Response**, Select *Add default response*.
    i. **Headers:** 'Content-Type application/json'
    ii. **Body:** *copy and paste .json from [IP Context Object Example.json](https://github.com/ERackIT/Sentinel/blob/main/Logic%20Apps/Spur/Create%20Custom%20Connector/IP%20Context%20Object%20Example.json)
14. Select **Import**
15. At the top of the page, select **Update Connector**.

**Reference:** [Postman | MS Learn](https://learn.microsoft.com/en-us/connectors/custom-connectors/define-postman-collection)
