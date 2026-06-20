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
After creating our users, we need to add them to groups for simplified management. The table below are my users that I added.

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

7. I did the same for Dragon, Adi, Dim, and Jeff.

## Role Changing (Mover)
After a few years of working as a Software Engineer, John had learned a lot about AppSec as he went by. He had been promoted to an AppSec Engineer.
As the IAM Administrator, it is your job that John moves from the "Engineering" Department to the "Security" Department smoothly.

1. Go to Users -> John Green -> Edit Properties -> Job Information
2. Change his `Job Title` to AppSec Engineer
3. Change his `Department` to Security
<img width="850" height="615" alt="image" src="https://github.com/user-attachments/assets/9ca664d3-a758-404c-abce-61384bc814cf" />

When these attributes change, John should be automatically removed from the Engineering Group and added to the Security Group
<img width="517" height="210" alt="image" src="https://github.com/user-attachments/assets/1b0e4a37-8a0e-465c-8d26-93e6edf8494c" />

## Employee Termination (Leaver)
After working as an AppSec Engineer, John had decided he had made enough money and retired from Gitty Solutions.
As the IAM Administrator, it is your job to correctly offboard John from Gitty Solutions.

**Step 1: Disable the Account**

1. Go to Users -> John Green -> Account Status -> Uncheck Account Enabled
<img width="285" height="312" alt="image" src="https://github.com/user-attachments/assets/7021a0a0-4409-421d-a8b5-bcbde9225aa6" />

**Step 2: Revoke Active Sessions**

2. Go to Users -> John Green -> Revoke Sessions -> Click Yes
<img width="844" height="158" alt="image" src="https://github.com/user-attachments/assets/45479b5e-457d-4f1b-bfe7-789bd4b295b7" />

**Step 3: Remove Group Memberships**
3. Go to Users -> John Green -> Edit Properties -> Job Information -> Remove Job Title and Department. This will remove him from the group because of the dynamic assignment. Note: I tried to remove John Green
using the "Remove membership button", but it said I had insufficient privileges, so I used this method instead.

**Step 4: Archive User Data**
Since this is only a lab user without any real data, there isn't anything to really "Archive". If John hypothetically did have OneDrive/Sharepoint or other sorts of data on the account, we would archive it by transferring the ownership of the files to a manager/secondary owner that will hold onto the data until account is deleted (after the retention period). We could do this by:
1. Go to Microsoft 365 Admin Center -> Users -> Active Users -> Select John Green -> OneDrive
2. From there, you would be able to move the ownership of the files to an appropriate account/manager (Nothing shows up here since there was never anything in John's account in the first place)
<img width="552" height="323" alt="image" src="https://github.com/user-attachments/assets/7f6088a2-ed44-4a79-86d8-53963b76d069" />

**Step 5: Delete Account after Retention Period**
1. Go to Users -> John Green -> Delete John Green
2. This is only considered a soft delete. Entra will permanently delete the user after 30 days, but if you want, you can delete the account immediately by navigating to "Deleted Users"
<img width="586" height="331" alt="image" src="https://github.com/user-attachments/assets/69aed152-aa77-4a22-8c38-b4c67e13ea8e" />

3. By selecting "Delete Permanently", he will be gone forever. Goodbye John!

## JML Diagram
<img width="432" height="571" alt="image" src="https://github.com/user-attachments/assets/4d219d0e-2ecd-42b2-a0d9-0dc50fa4da38" />

# Reflection
Through this project, I gained hands-on experience with Microsoft Entra ID and learned the fundamentals of Identity and Access Management (IAM) by simulating the Joiner, Mover, and Leaver (JML) process. Creating, modifying, and disabling user accounts helped me understand how organizations manage identities throughout an employee's lifecycle and ensure appropriate access is maintained at each stage. I also became familiar with basic navigation within the Entra ID portal, including managing users, groups, licenses, and audit logs. Additionally, documenting the JML workflow through a diagram reinforced the importance of structured onboarding, role changes, and offboarding processes in reducing security risks and supporting effective access control within an organization.

