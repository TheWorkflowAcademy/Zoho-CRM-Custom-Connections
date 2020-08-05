# Zoho CRM Custom Connections
This tutorial will walk you through creating custom connections in Zoho CRM.

This tutorial will not be teaching underlying technologies such as OAuth 2.0. To learn more about how to implement OAuth 2.0 in Zoho CRM, see this GitHub Repository: [Deluge OAuth 2.0 Client](https://github.com/TheWorkflowAcademy/Deluge-OAuth-2.0-Client).

## Introduction
Zoho CRM gives you the ability to create high ROI integrations to your software tools. Zoho created the Deluge scripting language to quickly connect your data. One way this is done is via [Connections](https://www.zoho.com/crm/developer/docs/connectors/). These connections simplify complex API authentication workflows into using a simple *connection* parameter in your API call.

Below is an example of an API call to Zoho CRM using a connection parameter:
```javascript
getContact = invokeurl [
  url: "https://www.zohoapis.com/crm/v2/Contacts/2787502000001234567"
  type: GET
  connection: "zoho_crm"
];
```

This connection to Zoho CRM from Zoho CRM (sooooo meta, right?) is part of the prebuilt *Zoho OAuth* connection. Zoho has provided a number of out-of-the-box connections to Shopify, Survey Monkey, MailChimp, and many other popular business software.

In this tutorial we will cover how to create a custom connection to a tool that Zoho has not built a connection for.
## Tutorial
### Getting Started
To access the Connections, do the following:
1. Go to the **Setup** page in Zoho CRM
2. Under Developer Space, click **Connections**
3. Click **[+ Add Connection]**

In the *Pick Your Service* tab you can browse for available connections. 

Let's head over to the *Custom Service* tab and see what's going on.

A few important first-observations:
- *Service Details* contains the naming and authentication info for the tool you are trying to connect to.
- *Connection Details* specifies the naming you will use in your Deluge scripts.

We're going to continue with an API that uses the OAuth 2.0 authentication framework. This is the most common method of authentication for major Open APIs.

### Creating OAuth 2.0 Parameters
Within the service you are trying to connect, follow the guide to generate a *Client ID* and *Client Secret* for your application. 

#### Redirect URIs
When creating your *Client ID* and *Client Secret* you will need to declare an authorized Redirect URI and often scopes. 

**Zoho CRM custom connections require that you add the following authorized Redirect URI:** *https://deluge.zoho.com/delugeauth/callback*.

#### Scopes
Many OAuth 2 APIs require each Client ID to be given a set of scopes (think: permissions and limitations) to promote data security. Each scope maps to a set of API endpoints. You should give each Client ID the least amount of scopes possible to successfully perform your integration. In order to find the scopes you need, consult your API reference (it is often referenced in the section discussing the Authorization Request).


### OAuth 2.0 URLs
OAuth 2.0 relies on the following URLs which the software service will provide in their API Reference:
1. **Authroize URL:** Makes Authorization Requests (Often ends with `/oauth2/auth`, `/auth`, or `/authorize`).
2. **Access Token URL:** Generates Access Tokens and Refresh Tokens (Often ends with `/oauth2/token` or `/api/token`).
3. **Refresh Token URL:** Generates Access Tokens with a Refresh Token (Often ends with `/oauth2/token` or `/api/token`).

### Creating the Connection in Zoho CRM
1. Go to your Connections in Zoho CRM
2. Click **[+ Add Connection]**, go to the **Custom Service** tab, then select **Create Your Own**.
3. Enter the following field mapping:

      **Service Name:** [The name of the service you are connecting (e.g., Hubspot, Survey Monkey).]
      
      **Service LinkName:** [The name of the service you are connecting without sapaces (e.g., hubspot, survey_monkey).]
      
      **Authentication Type:** oAuth2
      
      **Param Type:** Header
      
      **Grant Type:** Authorization Code
      
      **Client Id:** [Client ID registerd in the software service.]
      
      **Client Secret:** [Client Secret generated along with your Client ID]
      
      **Authorize Url:** [Authorize URL OAuth 2.0 endpoint provided in your service's API reference.]
      
      **Access Token Url:** [Access Token URL OAuth 2.0 endpoint provided in your service's API reference.]
      
      **Refresh Token Url:** [Refresh Token URL OAuth 2.0 endpoint provided in your service's API reference.]
      
      
      **Connection Name:** [The name of the connection. If you plan to create multiple connections for a Service, name it differently than the Service Name (e.g., Hubspot Accounts, Survey Monkey).]
      
      **Connection LinkName:** [The name of the conneciton that will be used in Deluge scripts (e.g., hubspot_accounts, survey_monkey).]
      
      **Scope:** [Enter the requested scopes one-by-one (be sure to click the plus sign).
      
      **Scope Delimiter:** [The character between each of your scopes. This only appears when multiple scopes are entered. Most common is a space, but consult your API reference for more information.]
      
4. Select **Create and Connect**.
5. Follow the authorization prompts from your service.


### Connection Usage
After your connection is created, Zoho will generate an `invokeUrl` statement to be used in your Deluge code.

It should look something like this:
```javascript
response = invokeUrl [
    url : <url>
    type : GET/POST/PUT/DELETE
    parameters : <paramMap/string>
    connection : YOUR_CONNECTION_NAME
];
```
Sometimes the Deluge editor doesn't like your `connection` name, in which case surround it with quotations like `'YOUR_CONNECTION_NAME'`. As long as you have the permissions, you are now able to make an API call to any software you need.


**You should now be connected to your custom service!** There are some services which for whatever reason do not play well with Custom Connections. If this is the case, reach out to us. You may also consider building your own OAuth 2.0 workflow in Deluge, in which case you may reference the following repository: [Deluge OAuth 2.0 Client](https://github.com/TheWorkflowAcademy/Deluge-OAuth-2.0-Client). 

**If you ran into any issues or have any questions, please do not hesitate to reach out at https://theworkflowacademy.com/get-help/.**


