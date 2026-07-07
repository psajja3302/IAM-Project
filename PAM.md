# Privileged Access Management (PAM)
By now, Gitty Solutions has significantly improved its identity security posture since the beginning of the company. However, a recent internal audit identified a new concern; several IT administrators maintain permanent administrative privileges, even when they **aren't actively performing administrative tasks**.

If an administrator's account was compromised through phishing, malware, or other attack method, an attacker would be able to inherit administrative privileges, such as accessing sensitive information/resources.

To reduce this risk, the IAM team has decided to implement **PAM** using Entra's Privileged Identity Management (PIM) system. Administrators will receive eligible role assignments only when required to perform administrative tasks, also know as **Just-In-Time (JIT) access**.

## Configure JIT
Since we have been working with Dim and Jeff Green's accounts the past few labs, we will be using his account again this time. Since he has administrative privileges (Helpdesk Administrator/User Administrator), we must configure PIM with them.

1. From the Entra admin center, scroll down on the left hand bar until you see ID Governance. Click on the tab, and you will see **Privileged Identity Management**. Click on that.
2. On the left hand side, we can see Tasks, Manage, Activity, and Troubleshoot. Click on "Microsoft Entra roles" under Manage.
3. Click on "Assign Eligibility". This will activate JIT access to select roles.
4. In the search bar, search up "Helpdesk Administrator" and click on it.
5. Click on "Add Assignments", and under "Select members", click on Dim Green (Helpdesk Administratror)
6. From here, you can navigate to "Settings" in the same tab, and make sure the assignment type is set to "Eligible".

<img width="573" height="445" alt="image" src="https://github.com/user-attachments/assets/0cee74da-2da4-4525-8b72-a82347e8eef4" />

7. Save these settings, but we need to configure more. Navigate to "Role Settings" of Helpdesk Administrator. Configure the settings I have set below. These settings ensure that the right person is accessing the account, , the person has proper justification for why the account needs to be accessed, and a maximum duration of time is established.

<img width="602" height="729" alt="image" src="https://github.com/user-attachments/assets/ae51d431-9611-428a-be84-f2d0fc0dfe16" />

<img width="460" height="341" alt="image" src="https://github.com/user-attachments/assets/010543fe-91c5-4b0e-b929-e3d261ad7f9f" />

8. Save these updated settings

## Testing PIM Configuration
Now that we have configured the PIM settings for Helpdesk Administrator for Dim Green, we will now test the user Dim Green by signing in. (Note: Before signing in as this user, I removed them from the `RBAC-IT-Admin` group, as it will interfere with the PIM settings)

1. After logging into Dim Green, navigate to PIM settings

<img width="1560" height="322" alt="image" src="https://github.com/user-attachments/assets/9c3ed04e-b7b9-42c1-8f4a-9af8a988eeaa" />

2. Click on "Activate" next to Helpdesk Administrator

<img width="589" height="872" alt="image" src="https://github.com/user-attachments/assets/3b511bb0-a405-4256-9ca3-015a101224ed" />

3. As we can see, the role assignment is now active. The MFA prompt would be given if your current Azure session has expired. Since I used MFA to sign into this account just a few seconds ago, it would not prompt me again.

<img width="1248" height="117" alt="image" src="https://github.com/user-attachments/assets/3d9ae80a-de0a-4e05-982b-30b05cc30eb5" />

## Auditing
By going to "My audit history" in PIM, we are able to see the actions that have happened regarding the roles that were set up.

<img width="1579" height="509" alt="image" src="https://github.com/user-attachments/assets/2db88b8e-6331-4167-8ec6-c00839a7d19b" />

# Reflection
This project demonstrated how Entra's PIM implements JIT access by replacing permanent administrative assignments with eligible assignments that require activation. I configured an administrator role to require MFA, a relevant justification, and a limited activation duration before the role privileges were granted. This approach reduces the risks associated with permanent privileges because administrative access exists only when needed. Implementing PIM in Entra reinforced my understanding of the principle of least privilege and how PAM strengthens an organization's overall security posture by minimizing the attack surface for attackers to misuse privileged accounts.

## Next Steps
Please move to the `Access Reviews.md` file next.






