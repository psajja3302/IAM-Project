# Identity Monitoring
Gitty Solutions recently completed several identity security improvements, such as:

- MFA deployment
- RBAC implementation
- Privileged Identity Management
- Access Reviews


Leadership now wants continuous monitoring to detect suspicious authentication activity before an account is compromised.

## ID Protection
From the Entra admin center, scroll down on the left hand side and navigate towards **ID Protection**.

<img width="1620" height="837" alt="image" src="https://github.com/user-attachments/assets/cc468e2d-fa74-4718-908a-e78bf035ad97" />

To learn more in-depth about ID Protection, you can read this article here: ([ID Protection](https://learn.microsoft.com/en-us/entra/id-protection/overview-identity-protection)). Essentially, Microsoft's 
ID Protection uses a broad range of signals to identify risky behaviors, and you can investigate these behaviors in the ID Protection tab. As we can see, we already generated attacks from our previous 
lab (See ```Deploying MFA.md```) where I used Tor Browser to log in as Jeff Green into Microsoft apps. Tor masks your IP address and location, and Entra flagged this as "Anonymous IP Address" as seen below.

<img width="1324" height="434" alt="image" src="https://github.com/user-attachments/assets/95886a1f-28e0-4c02-968f-ffbaae203f1b" />

## Sign-In Logs
From the Entra admin center, scroll down on the left hand side and navigate towards **Monitoring & health**. From here, we can see many types of logs, but we want to focus on the **sign-in logs**.

<img width="1100" height="584" alt="image" src="https://github.com/user-attachments/assets/70a8c570-fb49-42bd-8ad1-1385f58f491d" />

By clicking on the date, you can see all the metadata of that log.

If you click on Download -> Export to CSV, we can use Python to analyze these logs, which we will be doing later in a different file.

## Audit Logs
From **Monitoring & health**, navigate towards **audit logs**.

<img width="1143" height="826" alt="image" src="https://github.com/user-attachments/assets/8dc0372d-7bdc-43a8-b06f-00ca6fa8424c" />

By clicking on the date, you can see all the metadata of that log. I analyzed the first log, which was titled "Validate user authentication". In the log, I was able to see that I was the target user, illustrating that I had 
recently logged in.

<img width="565" height="137" alt="image" src="https://github.com/user-attachments/assets/95ea3799-3d51-4a2e-9edc-904ebb20d936" />

We can also similarly export this log data as a CSV file and then use Python to analyze these logs. We will also be doing this in a different file.

# Reflection
This project demonstrated how Entra's ID Protection provides visibility into authentication activity. I reinforced my understanding of how to investigate and interpret login events/audit logs by reviewing user identities, IP addresses, locations, 
MFA status, Conditional Access outcomes, etc. This project also reinforced the importance of continuous identity monitoring as part of a defense-in-depth IAM strategy.
