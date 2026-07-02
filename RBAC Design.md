# RBAC Design 

As Gitty Solutions has expanded in the past 2 years, reaching over 100+ employees, administrators realized one point: The groups that they established at the beginning of the company do not provide any permissions. They are purely organizational. This is not **least privilege**, it was just labelling.

As the IAM administrators reflect, they introduce Role-Based Access Control (RBAC) by mapping each department group to a defined permission set, assigning those permissions through Entra built-in roles, and verifying those controls.

| Phase 1 | Phase 2 |
|---|---|
| Groups are organizational labels | Groups carry role assignments |
| All users have equivalent Entra access | Permissions are scoped by department |
| JML process manages identity | RBAC manages what that identity can do |
| Dynamic groups | Role-assignable groups |

Mapped RBAC Roles
| Department | Phase 1 Group | Phase 2 RBAC Group | Entra Role Assigned |
|---|---|---|---|
| IT Operations | `Engineering` (dynamic) | `RBAC-IT-Admins` | Helpdesk Administrator |
| Human Resources | `HR` (dynamic) | `RBAC-HR` | User Administrator |
| Finance | `Finance` (dynamic) | `RBAC-Finance` | *(none — read only)* |
| Security | `Security` (dynamic) | `RBAC-Security` | Security Administrator |
| Engineering | `Engineering` (dynamic) | `RBAC-Standard-Users` | *(none — baseline)* |

As you can see, Phase 1's dynamic groups remain for organizational structure, while Phase 2 implements security groups specifically for permission management.

## Why RBAC over Direct/Ad Hoc Assignment
**Auditing**: When viewing audit logs, removing someone from group is much easier to spot than several direct role assignments removed at different times, especially when scaled to a large corporation

**Control**: When users move between groups, particularly RBAC groups, the mover workflow will adjust permissions automatically.

**Least Privilege**: With Ad Hoc approaches, you may find a user "privilege creeping", where that user has accumulated too many permission as they were constantly changing roles. RBAC controls this by enforcing least privilege, where the user has the least amount of access required to perform their job.

## Establish RBAC Groups
The company recently hired several new employees for different departments. Rather than assigning permissions directly to each employee, the IAM team creates role-assignable security groups that represent job functions.

1. Go to Entra ID -> Groups -> New Group
2. Set up the group settings like how I did in the image below:

<img width="693" height="497" alt="image" src="https://github.com/user-attachments/assets/6dd35ab8-6f91-423a-aafe-2bd0edc68e13" />

3. Add the appropriate member(s) to the group
4. Repeat for each group using the mapping table (Mapped RBAC Roles) above
5. After completing the creation of all groups, you should be able to see them in the "Groups" tab

<img width="968" height="212" alt="image" src="https://github.com/user-attachments/assets/6aecaa88-4322-474a-8bba-dc68d6cb16b9" />

6. After clicking on a group, you should be able to see the correct user assigned (Please refer to the **UserLifecycleManagement** markdown file)
<img width="726" height="360" alt="image" src="https://github.com/user-attachments/assets/af3bfabe-59f6-4e32-975e-076c03176e29" />

## Verify Controls - Access Testing
Sign in as each test user and confirm the permission boundaries hold. Make sure the RBAC is performing as expected. Below, I tested users Dim Green and Jeff Green, who are Helpdesk and User Administrators respectively. I tested them on the user John Green, who is assigned to the RBAC-Standard-Users group. Please note that you must use the authenticator app to sign into each account.

**Dim Green**
1. Should be able to reset another user's password and manage MFA registration
<img width="1346" height="432" alt="image" src="https://github.com/user-attachments/assets/ecfcf53b-7c8e-457c-86f6-73aacd189fc0" />
Initially, I was not able to reset John Green's password, and this was because he was assigned a group membership (RBAC-Standard-Users). By removing the group membership, I was then able to reset his password. I noted that the Engineering group did not affect the ability to reset a password.

<img width="1366" height="394" alt="image" src="https://github.com/user-attachments/assets/4454ca05-e3f6-40e5-ba11-d1a1545ac615" />

2. Should NOT be able to create a new user or assign a role to a user
<img width="1365" height="239" alt="image" src="https://github.com/user-attachments/assets/5fbe73b5-439c-4c29-9e17-c78d1668b739" />


**Jeff Green**
1. Should be able to create a new user through the portal
<img width="1362" height="237" alt="image" src="https://github.com/user-attachments/assets/25cb70f9-6aa4-45a9-a123-0a367a14c1de" />

2. Should NOT be able to modify Dim Green's account, since User Admins cannot touch privileged accounts
<img width="1352" height="314" alt="image" src="https://github.com/user-attachments/assets/654ed6f2-6197-4198-9831-f86335421a2c" />

One thing to note is that I am able to modify Dim Green's basic information, such as display name, first/last name, and user type, but nothing else.

## Joiner/Mover Demonstration
Jerry Chen joins the IT department as a new helpdesk worker. Instead of assigning adminstrative roles/permissions directly to Sarah, the IAM team follows the company's new RBAC policy. The team wants you to:
1. Create the user Jerry Chen
2. Add him to the RBAC-IT-Admins group
<img width="492" height="770" alt="image" src="https://github.com/user-attachments/assets/d5c92842-7b0d-4f8e-a065-d1942da21a6b" />


After a few months, Jerry decides it's time for a career change and gets recruited by the Finance department. Gitty Solutions must ensure that she no longer has elevated privileges
1. Remove Jerry from the RBAC-IT-Admins group and add her to the RBAC-Finance group
<img width="674" height="238" alt="image" src="https://github.com/user-attachments/assets/b9c406af-74bf-4498-a1ca-9524994f1806" />

2. Verify the Helpdesk Administrator role is removed
<img width="725" height="264" alt="image" src="https://github.com/user-attachments/assets/80d8edb1-895f-482c-b04a-4dde837451a4" />

# Reflection
Through this project, I expanded on the identity foundation I built in Phase 1 (User Lifecycle Management) by implementing Role Based Acces Control (RBAC). Designing these role-assignable security groups and mapping them to built in Entra roles helped me understand how organizations enforce least privilege at a scale while minimizing/eliminating privilege creeping. Testing the controls hands-on as Dim Green and Jeff Green reinforced my understanding of Entra's privilege protection. Additionally, Jerry Chen's onboarding and department transfer demonstrated how RBAC makes access changes automatic and easily autiable.

## Next Steps
Please move to the `Deploying MFA.md` file next.
