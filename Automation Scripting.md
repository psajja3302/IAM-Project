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
1. After registering the application, click on **Certificates and Secrets** on the left hand management side. Create a new client secret and copy that value
2. Now, navigate towards **API Permissions**. Click on "add permission" and select **Microsoft Graph**. Click on "delegated permissions". You will now be able to select a tremendous amount of permissions, but we only need a few for basic scripting. The permissions below are the ones we will add, and explanations are written alongside them.

| Permissions | Explanation |
| --- | --- |
| User.ReadWrite.All | Allows you to create and delete users |
| Group.Read.All | Allows you to pull groups and read them |
| GroupMember.Read.All | Allows you to read group memberships within a group |
| AuditLog.Read.All | Allows you to read sign in logs and authentication events |




