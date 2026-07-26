# Automation Scripting with Entra ID

As Gitty Solutions expands even further, the IAM team decides that they cannot continue manually execute IAM tasks without sacrificing efficiency. Therefore, they have decided to use Python to create scripts to automated menial tasks in Entra, such as creating users, querying sign-in logs, etc.

## Package Installation

We need to install three packages: `msgraph-sdk`, `reportlab`, and `pandas`. 

```pip install msgraph-sdk```

```pip install reportlab```

```pip install pandas```

## App Registration

In Entra's Admin Center, navigate towards App Registrations on the left hand side. Create a new registration. We won't need a redirect URI.

<img width="882" height="440" alt="Screenshot 2026-07-26 at 3 25 32 PM" src="https://github.com/user-attachments/assets/61cf75e1-a3c9-4f90-9de7-09a7a9bef877" />

Register the application.
1. After registering the application, click on **Certificates and Secrets** on the left hand management side. Create a new client secret, and copy and paste that value somewhere safe; it only appears once.
2. Now, navigate towards **API Permissions**. Click on "add permission" and select **Microsoft Graph**. Click on "delegated permissions". You will now be able to select a tremendous amount of permissions, but we only need a few for basic scripting. The permissions below are the ones we will add, and explanations are written alongside them.

| Permissions | Explanation |
| --- | --- |
| User.ReadWrite.All | Allows you to create and delete users |
| Group.Read.All | Allows you to pull groups and read them |
| GroupMember.Read.All | Allows you to read group memberships |
| AuditLog.Read.All | Allows you to read sign in logs and authentication events |

Make sure to **Grant admin consent for Home**, otherwise every API call will fail.

Essential data that we will be using is the Tenant ID, Client ID, and Client Secret, which will be shown at the top of the **Overview** page for the app.

<img width="916" height="149" alt="image" src="https://github.com/user-attachments/assets/035f1208-61e5-4e9d-bf98-0eadb2f9fd3e" />

## Script

The script can be accessed via the **master** branch titled `iamauto.py`. The script has 5 methods, each serving different functions.

# Reflection

This project demonstrates automation can further improve common identity and access management tasks that are often performed manually through the Microsoft Entra admin center. These scripts I created allowed the automation of provisioning/disabiling users, retriving privileged group membership, aggregating and analyzing sign-in activity, and generating management reports. I was able to gain hands-on experience with OAuth authentication, Entra's app registrations, Microsoft Graph permissions, and least-privilege design. Integrating these automation workflows with reporting reinforced my understanding of how scripting can improve operational efficiency, reduce human error, and support security auditing in enterprise IAM environments.
