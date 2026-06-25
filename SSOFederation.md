# SSO/Federation 

## Integrating a SaaS from Entra's Enterprise Application Gallery
From here onwards, I will be using Entra's Admin Center for this file and the next few as well. On the left side of the Admin Center, we want to focus on the Entra ID subsection.

**Step 1: Enterprise Apps -> New Application -> Select "Salesforce" -> Create**
- From this step, you should be able to create the Salesforce application, where we will be able to configure SSO from here.
<img width="1097" height="585" alt="image" src="https://github.com/user-attachments/assets/c1b52067-c088-4273-a843-2456e495c3c4" />


**Step 2: Set up SSO**
- Click on "2. Set up single sign on"
- With Salesforce, there are 3 SSO methods provided. We will pick SAML.
- Configure your Identifier, Reply URL, and Sign on URL

Identifier: The unique name of the application you are identifying into. If you don't match the Entity ID, then the session won't be established

Reply URL: The location Salesforce wants Entra to send the SAML assertion after login.

Sign on URL: Where users start the login process

**Step 3: Create Salesforce Account + Setup**

In order to configure your identifier, reply url, and Sign on URL, you need a Salesforce Developer Account
- Search up "Salesforce Developer Edition" on Google and create a free account
- After making an account and signing in, in the top right, click on the Gear icon and select "Setup"
- In the quick search bar, search up "My Domain"
<img width="661" height="74" alt="image" src="https://github.com/user-attachments/assets/29d9e50f-891d-42ce-86e5-82d60a95ba2e" />

Sign on URL = Current My Domain URL

- In the quick search bar, search up "Single Sign-On Settings"
- On Entra ID Saleforce SAML Settings, download the Federation Metadata XML (Under 3. SAML Certificates)
- On Salesforce, click the "Download Metadata" button and import the Federation Metadata XML file into here

Identifier + Reply URL = Entity ID
<img width="1329" height="98" alt="image" src="https://github.com/user-attachments/assets/0bca49fa-4473-4c38-80be-99b794141283" />


**Step 4: Test SSO**

Method 1: Test from Entra 
- From Entra, click on the "5. Test single sign-on with Salesforce" button
- Click test Sign In
- If it works, you'll land in Salesforce without entering Salesforce credentials.

Method 2: Test from Microsoft Apps
- From Entra, make sure your email/user is assigned to the app.
- Open https://myapplications.microsoft.com/
- Salesforce should appear in your applications here. Click it, and sign in.
- If it works, you'll land in Salesforce without entering Salesforce credentials.

## Building a Flask App
Not only can we configure SSO through the built in library, we can also create our own, custom SSO application through Entra ID. I won't be going through this, but you can get an idea of how to do so through these links:
1. https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings
2. https://learn.microsoft.com/en-us/power-pages/security/authentication/configure-site#select-general-authentication-settings
3. https://learn.microsoft.com/en-us/power-pages/getting-started/create-manage

After following these steps, you can create a flask app by importing the flask module and msal (Microsoft Authentication) module
```pip install flask msal```

If your code is properly created, you should be able to login via your Entra ID Account.

## Next Steps
