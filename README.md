# Microsoft Entra ID IAM Project

This hands-on Identity and Access Management build simulates the full identity lifecycle for Gitty Solutions, a fictional company that grows from <10 to 100+ employees over the course of the project. This project chains together seven core IAM disciplines into one continuous scenario — the same test users and groups created in the first lab are still being managed, reviewed, and monitored in the last one. 

Everything is built inside a free Entra ID P2 trial tenant.

## Skills Demonstrated

Read in this order — later files assume the groups, users, and roles set up in earlier ones:

1. **`UserLifecycleManagement.md`** — Onboarding, role changes, and offboarding (Joiner/Mover/Leaver), with dynamic groups tied to department attributes.
2. **`SSOFederation.md`** — SAML SSO into Salesforce, plus a note on federating a custom app with Flask/MSAL.
3. **`RBAC Design.md`** — Replacing purely organizational groups with role-assignable groups mapped to least-privilege Entra roles.
4. **`Deploying MFA.md`** — MFA rollout in two phases: Security Defaults baseline, then targeted Conditional Access policies for admins and risky sign-ins.
5. **`PAM.md`** — Just-in-time privileged access using Entra PIM, so admin rights only exist when they're actively needed.
6. **`Access Reviews.md`** — Recurring self-attestation and manager-approval reviews that keep privileged access current.
7. **`Identity Monitoring.md`** — Identity Protection, sign-in logs, and audit logs for ongoing detection.

Each file ends with a short reflection on what the exercise reinforced.

## Setup

1. Create a free Azure account (payment card required for verification).
2. From Microsoft Entra ID, activate a free **Entra ID P2** trial — this is required for MFA/Conditional Access, PIM, and Access Reviews later on.
3. Start with `UserLifecycleManagement.md`.
