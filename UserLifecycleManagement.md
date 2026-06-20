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

## Entra ID P2 Free Trial
1. Google "Microsoft Entra ID P2"
2. Select "Try for free" for the Microsoft Entra ID P2 plan
3. You can select up to 25 free users. You will not be charged if you cancel the trial before the date.
4. After purchase, you can use either the Entra admin center or through Microsoft Azure. At the start, I used Azure.

## Hire New Onboarding - Quick Create Users
As the IAM administrator, it is your job to understand how to create and add users to your organization, also known as the onboarding process. You are hiring 5 fresh employees this season.
1. On the Microsoft Entra ID page, scroll down to view quick actions. Click on `Add User`. Create 1-2 users manually.
2. If you have the Microsoft Entra Suite, you can enforce password complexity by going to `Microsoft Entra Password Protection` and set rules
3. You can assign properties to each user, such as job information, department, etc.
4. You can make your group/role assignments as well, but we don't need that as of now
5. After creating the user, go to Default Directory -> Manage -> Users, and you will be able to see the new user you created
<img width="260" height="144" alt="image" src="https://github.com/user-attachments/assets/47f7dc01-a515-4d49-bb3f-c022709afa6a" />

## Hire New Onboarding - Bulk Creating Users (CSV)
On Google Sheets or Microsoft Excel, create and import the remaining users using a CSV import. You can do this by:
1. Go to Default Directory -> Manage -> Users -> Bulk Operations (Top bar) -> Bulk create users
2. Here, you will see the option to download the csv template. Install it, fill in the template (I did this from Google Sheets), save as CSV (UTF-8), and then upload the file back into Entra ID. Note that the only pertinent information that needs to be filled out are the first 6 columns.
3. The Users section will automatically populate after submitting the file
<img width="274" height="266" alt="image" src="https://github.com/user-attachments/assets/027c067e-c795-441f-a5a2-b74ca44de68a" />

## Group Membership - Dynamic Assignment
After creating our users, we need to add them to groups for simplified management

| Name          | Job Title              | Department     |
| ------------- | ---------------------- | ---------------|
| John Green    | Software Engineer      | Engineering    |
| Dragon Green  | Security Engineer      | Security       |
| Adi Green     | Accountant             | Finance        |
| Dim Green     | SysAdmin               | IT Operations  |
| Jeff Green    | HR Specialist          | HR             |

1. Go to Default Directory -> Manage -> Groups -> All Groups -> New Group
2. Create a Group for each Department
3. For each group, select "Security" as the Group Type, Select Dynamic User
<img width="706" height="437" alt="image" src="https://github.com/user-attachments/assets/ffa8ffae-9bee-4a13-9d33-54629d77ce2f" />

4. Click Add Dynamic Query, which opens the rule builder
5. Add the rule for the group so that the users of a department are assigned to that department's group
<img width="1900" height="274" alt="image" src="https://github.com/user-attachments/assets/19fec29e-3646-47bf-bb9f-5869dd25620f" />

6. Since I had "John Green" assigned in the "Engineering" department, his account was autopopulated to this group
<img width="617" height="355" alt="image" src="https://github.com/user-attachments/assets/cea8dae8-6110-4a5f-a831-ed9774a06b38" />


