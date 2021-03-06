---
title: "MSAL Provider"
description: "Use msal.js to enable authentication and graph access for the Microsoft Graph Toolkit components"
localization_priority: Normal
author: nmetulev
---

# MSAL provider

The MSAL Provider uses [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js) to sign in users and acquire tokens to use with the Microsoft Graph.

Visit [the authentication docs](../providers.md) to learn more about the role of providers in the Microsoft Graph Toolkit

## Getting started

You can initialize the provider in HTML or JavaScript.

### In your HTML page

Initializing the Msal provider in HTML is the simplest method to create a new provider. Use the `mgt-msal-provider` component to set the client-id and other properties. This will create a new `UserAgentApplication` instance that will be used for all authentication and acquiring tokens.

```html
<mgt-msal-provider client-id="<YOUR_CLIENT_ID>"
                   login-type="redirect/popup"
                   authority=""></mgt-teams-provider>
```

> NOTE: `login-type` and `authority` are optional.

### In JavaScript

Initializing the provider in JavaScript allows you to provide more options`.

```ts
import {Providers, MsalProvider} from '@microsoft/mgt'
import {UserAgentApplication} from "msal";

Providers.globalProvider = new MsalProvider(config: MsalConfig);
```

where MsalConfig is:

```ts
interface MsalConfig {
  clientId: string;
  scopes?: string[];
  authority?: string;
  loginType?: LoginType;
  options?: Configuration; // msal js Configuration object
}
```

You must provide a `clientId` (to create a new `UserAgentApplication`)

To learn more about configuring Msal, visit the [Msal documentation](https://github.com/AzureAD/microsoft-authentication-library-for-js/wiki/MSAL-basics)

## Creating an app / Client Id

Visit the [Microsoft identity platform documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) to learn more about creating a new application and retrieving a clientId.

> Note: Msal only supports the Implicit Flow for OAuth. Make sure to enable Implicit Flow in your application in the Azure Portal (it is not enabled by default). Under `Authentication`, find the `Implicit grant` section and check both checkboxes for `Access tokens` and `ID tokens`
