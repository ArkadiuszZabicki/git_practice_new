# PagerDuty in One: Guide for Responders

- **Version:** 1.0.5
- **Last update:** 2020-10-13
## Your actions as first responder

[First responder flowchart](https://efficy-my.sharepoint.com/personal/arza_efficy_com/Documents/Microsoft%20Teams%20Chat%20Files/FirstResponder_Flowchart.png?web=1)

1. Make sure that a registered 'incident' exists in Pagerduty, or create a new one.
2. Acknowledge the alert and get online with your laptop. You are now interim 'Incident Commander'
    - If you for some reason are unable to investigate the alert - don't acknowledge, let it escalate instead.
3. Using all the tools at your disposal, spend a few minutes to try and figure out how serious the incident is, then set the Priority in PagerDuty. If you are unsure between [priorities](https://github.com/ApsisInternational/processes-and-policies/blob/main/04.%20Processes/Incident%20Process/APSIS%20One%20and%20APSIS%20Pro%20Incident%20Management%20Process.docx), set the higher value for now.
4. If, at any point you confirm that this is not a P1/P2 incident (but a false alarm or lower severity incident/bug) - see section “How to handle non-critical alerts” instead of following the steps below.
5. Determine if you need help from other responders, and if so, invite them through the “add Responder” function. If you are unsure, add “SOC Team on-call” and “Manager on-call” and someone will be along to help.
6. Create a new public Slack channel titled #inc-id-short_description where ID matches the PagerDuty ID. This can easily be done within Pagerduty by clicking the “set Slack channel” in the UI. All current responders will be automatically added to this channel, add any others that you want as well.
    - This can be accomplished through the native PagerDuty integration. Just click the “Set channel” link
7. Type into Slack: 'I am currently Incident Commander'
8. Write a short summary of what you know so far
9. Ask all present Responders to help set the correct Priority, then update in PagerDury if needed.
10. If the incident is still a [P1 or P2 after review](https://github.com/ApsisInternational/processes-and-policies/blob/main/04.%20Processes/Incident%20Process/APSIS%20One%20and%20APSIS%20Pro%20Incident%20Management%20Process.docx), immediately run the “Notify default stakeholders (this is a confirmed P1/P2 incident)” play in PagerDuty. This will add a few Teams to receive updates about the incident. 
11. (optional) At this point it’s fine to ask if any other Responder wants to take over the ICM role (e.g. if the incident is determined to be related to their domain more than yours). If nobody volunteers, you’re it. Normally the SOC team will be available to take over this role in order to allow you to focus more on solving the underlying issue

From here out, each incident will be handled based on how understanding develops. The gathered Responders constitute the Incident Response Team and will try their best to solve the issue.
- Add important discoveries or developments as Notes in PagerDuty. This makes it easier for late joining Responders to quickly recap the history.
- Share Subscriber Updates through PagerDuty “status updates.” This should be done regularly during the incident, at least hourly, even if no progress has been made since the last one.
    - Notes are for other Responders: they are intended to help other developers catch up
    - Subscriber Updates are for business stakeholders, customer support, and others. They should be about summarising the situation and letting non-technical stakeholders know what the impact is, what the status is, and if there is any progress, without requiring detailed technical knowledge. See section below for details on how to write updates
- Add more Responders or Subscribers as the situation warrants
- Once the emergency is handled, resolve the incident. Make sure to capture any follow-up actions or stories and send to respective backlog owners.
- Effort should be put into starting a draft of the Postmortem directly after (or even during, if possible) the incident has been handled (alternatively make sure all vital information is present in the Slack channel). This is to ensure that vital information is not lost. The draft should then be completed and ready for a Review during the next business day (see section “Post incident tasks”).

## Notes

Example of good Notes:
  - “DNS was incorrectly configured in AWS Centralised DNS account. Paging CloudEngineering for help.”
  - “Audience Export API is not responding for over 30 minutes and that causes delays in sendings. Audience team now looking at it.”

## Status updates

It’s important to remember that Status Updates will be broadcast to many people in the company with varying technical knowledge. If an incident is not affecting every customer, or only affecting a small % of customer data or functionality, it’s important to include this in the initial incident description and/or subsequent updates, to avoid unnecessary excitement.

When adding an update, try to make the update crisp and clear about the impact. Do not use “alarmist” language unnecessarily and try to include relevant details about the impact.

Example of a sequence of Subscriber Updates:
1. 22.04 Scheduled Email sendings are delayed by more than 30 minutes. Team is investigating. This affects all scheduled sendings for all customers.
2. 22.12 Possible root cause found in slow-running Audience exports. Impact probably limited to only a few customers with very large data volumes. Investigation continues.
3. 22.32 No further updates, teams are still investigating.
4. 23.32 No news yet, investigation on-going.
5. 00.11 Possible root cause found. Teams are creating a hotfix candidate and testing it.
6. 00.32 Hotfix verified. Deployment to production begun.
7. 00.45 Hotfix deployed and verified on production. Incident will be resolved.

Examples of suboptimal updates -- do not write updates like these:
 - “One is broken”
 - “Some services are down in Email”
 - “We are losing data for <customer> and maybe others too”

**At any point in the process, if you are lost or need help, add the Manager On-call escalation policy and one of us will be alerted**

## Post incident tasks (during next office-day)
1. For P1/P2: Complete the Postmortem and send it to the SOC-team for review. The SOC-team will now review, log and archive it
2. Complete bug reports and Stories that have been drafted during the incident so that they can enter the regular bug/feature/chore flow. Make sure respective BO are aware of the stories so that critical Stories can be completed as soon as possible.

## How to handle non-critical “incidents”

1. Make sure the incident is Acknowledged
2. If this is due to a bug that should be fixed (no false alarm or a “won’t fix bug”), set the priority of the Incident to P3-P5 and make sure that there exists a bug Story (create if no one exists yet). This report does not need to contain everything that is usually required for a proper bug report. See it more as a draft that you can expand upon during Office hours, but please make sure it contains a link to the Pagerduty incident so that more information can easily be added later.
3. See if you can add an “Event rule” that will suppress the alert so that this specific alarm does not trigger an incident again. Please only add such a rule if you’re sure that this will not risk suppressing critical incidents.
4. Mark incident as “Resolved”.
5. During next office-hours: Make sure you complete drafts of bug reports so that they can enter the regular bug-flow. If you’ve added a custom “Event rule” for this bug, please add a task on the Story that this rule should be removed after the bugfix has been deployed to production.
6. Copy the link to this Bug Story and paste it in the incident Slack channel (if one exists) or send to help-soc teams channel. The SOC team will now be responsible for communicating with Support and other stakeholders so that they are kept in the loop regarding customer-affecting issues.

# HOW TOs'

## Adding other team responders to an active incident

1. Open the incident in PagerDuty
2. Click 'add responder'
3. Select the desired teams escalation policy or a specific individual if you know they are needed.
4. Wait for them to acknowledge.

## Raising new incident manually

If you have noticed that some service or functionality from another team appears to be failing critically, but neither your or their alarms seem to be triggering alarms, you can use below steps to raise a new incident for that team manually.

**PLEASE NOTE** that this mechanism that this mechanism should only be used in case there is need for urgent attention on a high severity issue, a [P1 or P2 according to the process definition](https://github.com/ApsisInternational/processes-and-policies/blob/main/04.%20Processes/Incident%20Process/APSIS%20One%20and%20APSIS%20Pro%20Incident%20Management%20Process.docx).

For non-critical issues please consider other channels:
- If this is more a bug/problem, file a Shortcut ticket and ping the appropriate backlog manager via Teams or other means.

1. Open apsis.pagerduty.com
2. Open 'Services' list
3. Find the service from the team that's failing. If you don't know which one, use whatever looks reasonable from that team.
4. Open the service and click the New Incident button
5. Fill out the small form and raise the incident. Pick good Priority value and try to add a short but good description.
6. Wait for Responder to acknowledge.


