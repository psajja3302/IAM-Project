# User Lifecycle Management Simulation
You are the IAM Administrator for Gitty Solutions, a fictional software company with approximately 50 employees.
The company recently adopted a cloud-based identity provider and needs a standardized process for onboarding, role changes, and employee departures.
Your task is to manage employee identities throughout their lifecycle while enforcing least privilege and automated group membership.

Company Structure
| Department      | Purpose                    |
| --------------- | -------------------------- |
| Engineering     | Software development       |
| IT Operations   | Infrastructure and support |
| Human Resources | Employee management        |
| Finance         | Payroll and budgeting      |
| Security        | Monitoring and compliance  |


## Hire New Onboarding - Creating Users
As the IAM administrator, it is your job to understand how to create and add users to your organization, also known as the onboarding process. You are hiring 5 fresh employees this season.
1. On the Microsoft Entra ID page, scroll down to view quick actions. Click on `Add User`. Create 1-2 users manually.
2. If you have the Microsoft Entra Suite, you can enforce password complexity by going to `Microsoft Entra Password Protection` and set rules
3. You can assign properties to each user, such as job information, department, etc.
4. You can make your group/role assignments as well, but we don't need that as of now
5. After creating the user, go to Default Directory -> Manage -> Users, and you will be able to see the new user you created
<img width="260" height="144" alt="image" src="https://github.com/user-attachments/assets/47f7dc01-a515-4d49-bb3f-c022709afa6a" />

6. On Google Sheets or Microsoft Excel, create and import the remaining users using a CSV import
