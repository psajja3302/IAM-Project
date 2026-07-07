# Access Reviews
Gitty Solutions recently addded RBAC roles (See ```RBAC Design.md```) a few months ago, and the IAM team wants to ensure that all employees still require privileged access. They want to use recurring Access Reviews to verify that users still need group membership for privileged roles, remove unnecessary access to resources from users, and to uphold least privilege.

## Access Reviews on RBAC
Starting from the Entra admin center, we want to navigate to **ID Governance** like how we did in the ```PAM.md``` file, but this time, click on **Access Reviews**.
1. Click on "New access review"
2. Click "Review access to a resource type"

## Access Review: Self-Attestation
**Review Type**: 
- Select "Teams + Groups"
- "Select Teams + Groups"
- I selected my IT-Admins RBAC group, whose users have access to the Helpdesk Administrator role

<img width="847" height="538" alt="image" src="https://github.com/user-attachments/assets/b5d243c3-28ec-4cfb-9e36-a3979b42df4b" />

**Reviews**: 
- Select "Users review their own access", also known as self-attestation.
- The review for their access will last 7 days to allow them enough time, and this will occur annually indefinitely.

<img width="567" height="599" alt="image" src="https://github.com/user-attachments/assets/28682c0b-a333-4d1b-9b62-7d587c387e40" />

**Settings**: 
- Check off "Auto apply results to resource". This option allows Entra to automatically remove access for anyone who didn't respond or was denied, rather than having to manually remove access. At the end of the review, the review will be sent to me since I'm the Global Administrator

<img width="552" height="647" alt="image" src="https://github.com/user-attachments/assets/c27f1c43-a5ca-42f9-8fd5-597810ad97b6" />

**Review + Create**
- Use a relevant name (I used AR-RBAC-IT-Admins-Annually)

## Access Review: Manager Approval
**Review Type**: 
- Select "Teams + Groups"
- "Select Teams + Groups"
- I selected my HR RBAC group, whose users have access to the Users Administrator role

**Reviews**: 
- Usually, a manager may be in a different group or is a separate user on their own, or they would be labelled as such. Since I'm the lone Global Administrator, I'll just directly set the review up to myself.
- The review for their access will last 7 days to allow them enough time, and this will occur annually indefinitely.

<img width="501" height="197" alt="image" src="https://github.com/user-attachments/assets/c7f91e60-1a86-464f-bb65-0c1f43f1251b" />

**Settings**: 
- Check off "Auto apply results to resource". This option allows Entra to automatically remove access for anyone who didn't respond or was denied, rather than having to manually remove access. At the end of the review, the review will be sent to me since I'm the Global Administrator

**Review + Create**
- Use a relevant name (I used AR-RBAC-HR-Annually)

## Testing Access Review: Self Attestation
Dim Green -> Helpdesk Administrator

1. Sign into Microsoft Access (```myaccess.microsoft.com```) as the user (Dim Green for me). We can see the pending access review.

<img width="937" height="308" alt="image" src="https://github.com/user-attachments/assets/0222cee3-5ac3-4fa1-8409-adfe4b4aa427" />

Below, we can see the prompt:

<img width="576" height="507" alt="image" src="https://github.com/user-attachments/assets/5e134df6-8d68-4b6a-88f8-f6e733ab277b" />

After submitting, we will see that it is complete.

<img width="1623" height="298" alt="image" src="https://github.com/user-attachments/assets/ad1a35c2-091e-430b-ac31-c8502304af0c" />

## Testing Access Review: Manager Approval
Jeff Green -> User Administrator

1. Sign into Microsoft Access (```myaccess.microsoft.com```) as the manager. As we can see, we have a pending access review.

<img width="1440" height="366" alt="image" src="https://github.com/user-attachments/assets/58c66dda-b30f-4e41-b2ed-61c29f749802" />

Below, we can see the prompt:

<img width="1616" height="447" alt="image" src="https://github.com/user-attachments/assets/3bb2815f-09d3-40bc-88fa-8bcaa6e5a919" />

After submitting, we will see that it is complete. As an admin, I approved of their access rather than them doing it themselves.

## PIM Access Review
Alongside groups, we can also apply access review to PIM roles. Create a new access review from PIM.

ID Governance -> PIM -> Microsoft entra roles -> Access reviews -> New

Similar settings to the access reviews above...

<img width="808" height="704" alt="image" src="https://github.com/user-attachments/assets/164aedec-b2af-4af2-add5-090ca0c4fd49" />

However, since we are applying this with PIM, we want eligible assignment only since we made the role eligible only. This access review verifies that the user is still reasonably eligible for the role.

<img width="798" height="214" alt="image" src="https://github.com/user-attachments/assets/7824c298-f068-44c9-a028-8661a4e85a68" />

Besides that, the other settings are still the same.

<img width="809" height="459" alt="image" src="https://github.com/user-attachments/assets/8041446d-b4c6-47e5-9865-2104d38d439d" />

Save the results, and wait for the access review to initialize.

## Testing PIM Access Review
In PIM under Tasks, we can view the access review by clicking "Review access"

<img width="1636" height="327" alt="image" src="https://github.com/user-attachments/assets/d8a69220-73f9-4564-8035-2133917d83aa" />

After clicking AR-UserAdmin-Annually, I can now approve or deny the users who have access to the User Administrator role.

<img width="1628" height="597" alt="image" src="https://github.com/user-attachments/assets/1b42507e-47b2-489b-99aa-403ca852e195" />

# Reflection
This project introduced me to Access Reviews, a governance control that validates group memberships and privileged role assignments. I configured a recurring annual review for my RBAC groups using both self-attestation and manager approval, enabling automatic removal of users who failed the review. The users who fill out the access review are required to provide justification for their role. I also explored reviewing PIM-eligible role assignments, reinforcing the principle of least privilege. I learned a lot about how Identity Governance helps organizations maintain compliance by continuously validating access rather than granting permissions indefinitely. This project ties in with my ```RBAC.md``` and ```PAM.md``` portions.

## Next Steps
Please move to the ```Identity Monitoring.md``` file next.
