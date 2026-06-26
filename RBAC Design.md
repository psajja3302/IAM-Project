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
| Security | `Security` (dynamic) | `RBAC-Security` | *(none — future: Security Reader)* |
| Engineering | `Engineering` (dynamic) | `RBAC-Standard-Users` | *(none — baseline)* |

As you can see, Phase 1's dynamic groups remain for organizational structure, while Phase 2 implements security groups specifically for permission management.

## Why RBAC over Direct/Ad Hoc Assignment
**Auditing**: When viewing audit logs, removing someone from group is much easier to spot than several direct role assignments removed at different times, especially when scaled to a large corporation

**Control**: When users move between groups, particularly RBAC groups, the mover workflow will adjust permissions automatically.

**Least Privilege**: With Ad Hoc approaches, you may find a user "privilege creeping", where that user has accumulated too many permission as they were constantly changing roles. RBAC controls this by enforcing least privilege, where the user has the least amount of access required to perform their job.

## Establish RBAC Groups
The company recently hired several new employees for different departments. Rather than assigning permissions directly to each employee, the IAM team creates role-assignable security groups that represent job functions.

1. Go to Entra ID -> Groups -> New Group
