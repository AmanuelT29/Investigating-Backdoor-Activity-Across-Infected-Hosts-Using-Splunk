# Investigating-Backdoor-Activity-Infected-Hosts-Using-Splunk

## Scenario Details
SOC Analyst has observed some anomalous behaviours in the logs of a few windows machines. It looks like the adversary has access to some of these machines and successfully created some backdoor. My task as SOC Analyst is to examine the logs and identify the anomalies. All relevant logs are in the **index "main"**.

## Objective
In this investigation, I aim to identify and confirm potential indicators of compromise across suspected infected hosts. To do this, I will raise and methodically answer a series of key questions that guide each step of the process. This approach will help uncover any malicious activity, such as unauthorized account creation, suspicious command executions, or registry changes. The goal is to demonstrate how a structured analysis using tools like Splunk can be used to detect and respond to backdoor activity within a compromised environment.

---
### Question 1: Do the logs show that a new username was created?
To find the answer, I first checked the "Interesting Fields" pane, where I noticed that the EventID field was present. This indicates that logging was performed by Windows and/or Sysmon from the Sysinternals suite, as both use the EventID field to assign ID numbers corresponding to specific types of events. In this case, we're interested in events where a user account was created, which is recorded as **Event ID 4720**. I then ran the following search to locate these events: **index="main" EventID="4720"**

 ![Screenshot 2025-05-22 013046](https://github.com/user-attachments/assets/6db7cba7-2df6-4f6f-99b3-a3890e037118)
![Screenshot 2025-05-22 013239](https://github.com/user-attachments/assets/faa9e984-4aef-411b-a099-b812cd56eb0d)

As shown in the screenshot, only one event was returned, indicating that the account named **James** created the backdoor. It also reveals the name of the new backdoor account: **A1berto**. It's important to note the spelling—the letter "L" is replaced with the number "1", likely as an attempt to mimic the name of a legitimate user and avoid detection.
