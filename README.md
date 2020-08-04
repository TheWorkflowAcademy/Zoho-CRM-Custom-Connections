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

## Getting Started
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
