# RBAC Design 

As Gitty Solutions has expanded in the past 2 years, reaching over 100+ employees, administrators have noticed that permissions are being assigned directly to users. To improve security and 
simplify access management, the company decides to implement a Role-Based Access Control (RBAC) model in Microsoft Entra ID based on the principle of **least privilege**.

## Establish Administrative Roles
The company recently hired several new employees for different departments. Rather than assigning permissions directly to each employee, the IAM team creates role-assignable security groups that represent job functions.
