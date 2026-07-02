# Deploying MFA 

Gitty Solutions has recently experienced an increase in phishing emails targeting employees. During a routine security review, the IT department discovered that several employees reused passwords across personal and business 
accounts. While no accounts were compromised, leadership decided that relying solely on passwords no longer provides adequate protection for company resources.

To reduce the risk of unauthorized access, the IAM team has been tasked with implementing MFA across the organization.

The deployment will occur in two phases:

Phase 1: Enable Microsoft Entra Security Defaults to establish a baseline MFA policy across the tenant.

Phase 2: Replace Security Defaults with a Conditional Access policy that requires MFA for privileged administrative accounts, allowing greater flexibility while protecting the organization's most sensitive accounts.

## Phase 1: Security Defaults
Step 1: Go to Overview -> Properties -> Scroll down to **Manage Security Defaults**. This setting should be turned on already

<img width="540" height="759" alt="image" src="https://github.com/user-attachments/assets/ceaac68f-f97e-403c-8e3e-29db08aa545b" />

As we've seen before, when logging into created accounts, such as Jeff Green or Dim Green (refer to `RBAC Design.md`), we had to use the Microsoft Authenticator app on our phones (or other device) to login in. Security defaults
enforce MFA for all users. This is a minimal configuration, as there are no scopings, custom conditions, etc. As an organization matures, **Conditional Access Policies** are able to provide more granular policies.

## Phase 2 Part 1: Building Conditional Access (CA) Policies
Before starting, we need to turn off Security Defaults, as Entra blocks you if you try to enable a CA policy that utilizies MFA while this is on. Entra will ask you why you are disabling the defaults, just pick the option
that says something along the lines of "planning to implement Conditional Access Policies". After selecting this and disabling Security Defaults, it will take you to **Conditional Access**.

We will be creating two policies that trigger MFA in two separate ways: If the sign-in risk is medium/high, and if the user signing in is an administrator. We will be testing these polcies with Jeff and Dim Green.

Click on `Create new policy`

**Trigger MFA if Sign-In Risk is Medium or High**

Name: CA01-MediumHighRisk 

Users: Include Test Users (Dim Green, Jeff Green) or a security group containing them. (**NOTE: Always make sure to exclude one admin user so you don't get locked out of your own policy)

Target resources: All resources

Conditions > Sign-in risk > check Medium and High

Grant > Grant access > Require multifactor authentication

Enable policy: Report-only > On


<img width="315" height="692" alt="image" src="https://github.com/user-attachments/assets/07b59c52-8d67-47b6-a7c9-514154e3f97b" />

**Trigger MFA if Administrator Sign-In**

Name: CA02-AdminLogin

Users: Include a Directory Role (Helpdesk Administrator: Dim Green) (**NOTE: Always make sure to exclude one admin user so you don't get locked out of your own policy)

Target resources: All resources

Grant > Grant access > Require multifactor authentication

Enable policy: Report-only > On


<img width="313" height="835" alt="image" src="https://github.com/user-attachments/assets/82fd6c25-24d6-463d-a571-149934ab5767" />

## Phase 2 Part 2: Testing CA policies
First, we will be testing the **Administrator Login-In** policy. Open an incognito window and login into `https://myapps.microsoft.com` with the targeted user. In my case, it will be Dim Green. As we can see below, it works!

<img width="412" height="498" alt="image" src="https://github.com/user-attachments/assets/c8bb1701-9cbc-4bd4-9eed-19c257e6a5ea" />

By going to Conditional Access > Sign-in Logs, we can confirm that the policy had fired. Note: This will take a while to appear.

<img width="1630" height="355" alt="image" src="https://github.com/user-attachments/assets/0baf2ca6-a57c-4851-9431-866732acfaf6" />

Now, we will be testing the **Medium/High Sign-In Risk** policy. Open an incognito window and login into `https://myapps.microsoft.com` with the targeted user. In my case, it will be Jeff Green.
One documented method to test this medium/high risk sign in is to use the Tor Browser to mask your IP address. Entra flags Tor exit nodes as anonymous IP addresses because it's the same pattern malicious actors use to
mask sign-in origin. As I am using the `Brave Browser`, I can open a `New private window with Tor` instead of having to install Tor itself. You could also just install the Tor browser via `torproject.org`.

As we can see below, MFA was triggered. We can also see the policy successfully firing.

<img width="423" height="512" alt="image" src="https://github.com/user-attachments/assets/5b60f489-0a34-40fb-8a7f-1d9a424ddc28" />

<img width="1630" height="345" alt="image" src="https://github.com/user-attachments/assets/a9582c7a-38ad-476b-8b3b-e09be1d80e74" />

# Reflection
This project strengthened my understanding of how Microsoft Entra ID implements MFA, especially at different levels of organizational maturity. I learned the difference between Security Defaults, which provide a quick 
one-for-all baseline for MFA, and Conditional Access policies, which allow administrators to create targeted authentication requirements for specific users and roles. Configuring separate policies for administrator 
accounts and medium/high sign-in risk scenarios demonstrated how organizations can balance security with flexibility by protecting high-value accounts and responding to suspicious login activity. Testing the policies 
through normal administrator sign-ins and anonymous Tor-based logins also gave me practical experience validating that the Conditional Access policies were functioning correctly. It also reinforced my understanding of 
monitoring sign-in logs to verify policy enforcement and investigate authentication events.

## Next Steps
Please move to the `PAM.md` file next.


