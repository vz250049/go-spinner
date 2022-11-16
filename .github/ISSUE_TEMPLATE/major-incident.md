---
name: Major Incident
about: Use this template for major incidents resulting in an outage
title: Incident - [Description of incident]
labels: 'SEV-1, Incident'
assignees: ''
---

## Roles

**Incident Commander/SRE On-call:** This person is responsible to handle the incident end to end.

**Scribe:** This person handles all communications and reports to the required channels and to product management to communicate to customers.

**SME(Subject Matter Expert):** This person will be from the SRE team in case of Infrastructure related issues or application SME in case of application issues and sometimes both. They will focus primarily on investigating the issue during the incident.

## Step by step Response

### Initial Response - (5-10m)

Once **Incident Commander** receives the alert/issue through Pager Duty or through any other source(slack channel etc.) he/she should judge (see [To Incident, or not to Incident](https://confluence.ncr.com/display/SWDO/To+Incident%2C+or+not+to+Incident)) if this comes under the incident category or it's a known issue.
Once we quickly decide if this is an incident do the following tasks.

- [ ] Post in `#bsp-incidents-all` slack channel any information relevant to the alert
- [ ] Scribe should create a private slack channel to discuss the incident. The private slack channel name should be `inc-<dateofincident yyyymmdd>-<appname>` for example `inc-20210530-ias`.
- [ ] Start Outage bridge for the incident. Also, post this in `#bsp-incidents-all`.
- [ ] Use Pagerduty to page the other dev teammates using this [escalation policy](https://ncr-saas.pagerduty.com/escalation_policies#P52AVAS) and appropriate teams based on the component details.
Please refer to this [Monitors list with stakeholders](https://confluence.ncr.com/pages/viewpage.action?pageId=451401718) for contact details for relevant applications/components.
- [ ] Once all the required people join, **Incident Commander** must brief about the issue and should take inputs from other teams, SMEs and prepare initial analysis, impact, severity, etc.
- [ ] Scribe should take the notes of this discussion and prepare the draft for initial communications.

### Initial Communication - (5-10m)

- Once all the details like initial analysis, impact, severity, and other relevant details are collected by the Scribe, they need to send the communications to the following parties.
  - [ ] **Internal Stakeholders** - Please use the #bsp-incidents-all slack channel for internal communication and providing a C.A.N. report by using the format specified [here](https://confluence.ncr.com/display/SWDO/Sample+Templates). (*MOSTLY TECHNICAL*). or invoke BSP SRE Bot to generate CAN report with **!can** command
  - [ ] **Executive Leadership Team** - Please use the BSP SRE Bot to send-out ELT mail to Jerry or Mike with the **subject: Sev [1|2] | BSL [app_name] [full|partial] Outage**, so that then can send it directly to them once the content is approved. Sections specific in the ELT summary are important for visibility across NCR's leadership. (*BUSINESS IMPACT - NON-TECHNICAL*). We can invoke the bot with **!notify-elt** command. Refer [here](https://confluence.ncr.com/display/SWDO/Sample+Templates) to understand the ELT fields.
  - [ ] **External Stakeholders** - Now that we have an initial understanding of the issue, please go to [statuspage.io](http://statuspage.io/) to update the incident with details regarding the incident. This needs approval from leadership(Jerry/Jemmy/Mike) prior to submitting. We can make use of ELT Summary we used earlier. For now(until automation is done) updating status page can be done by the Scribe after approval.  
  **Note:** We will be providing a fully-fledged RCA after the incident, so please refrain from going too deep here and simply focus on providing business impact. (*BUSINESS IMPACT - NON TECHNICAL & NON CONFIDENTIAL*)

### Investigation and Triage

- [ ] While initial communication is being sent by the Scribe, the Incident Commander can start troubleshooting the issue with the SME. If there are any updates from the investigation the Incident Commander and SME will update the Scribe with any new information.  
**Note** Please see the below link for the severity-based matrix and communication windows. [Incident Severity Matrix](https://confluence.ncr.com/display/ncrsrem/Incident+Severity+Matrix)

- [ ] CAN Every 30 min for internal updates

- [ ] ELT Every 60 min for external updates, must be sent only for customer impacted services

- [ ] Do a real impact assesment 

- [ ] Update the statuspage to be accurate based on the current status of the incident

- [ ] During this phase, any relavant metrics must be updated on regular basis and work towards stabilizing the environment rather than finding the root cause by taking actions(with approval from SRE/Leadership). If any tickets need to be created Scribe/CommunicationsLead can help.

On a regular basis the Incident Commander will **evaluate the situation**, take help from SMEs, and page out to any other needed teams. They will also ensure the group remains focused on the current incident at hand.

**Communications should be sent out every 30 minutes. Add a comment to this issue to reflect when and what communications were sent.**

### Resolution

We've come to a conclusion for the incident, at least in the sense of stabilizing the environment. This phase is to close out any final actions or communications for the incident. It is important not to close the call right away, as there are things that can be important to keep a note of or required for future actions prior to problem management.

- [ ] **Final Actions - Incident Commander** needs to make any final actions now to complete stabilizing the environment. If any actions needed to be scheduled for a later time, discuss those now. (Scribe can take note in parallel).
- [ ] **Final Communication - Scribe** to collect final info regarding the incident (not RCA, that will come later). Final C.A.N, ELT and StatusPage updates to be sent out to respective stakeholders regarding the current state of the environment (expecting all is up and functional at this point).
- [ ] **Close incident/Bridge** - if not done already close the Pagerduty and/or Dynatrace alerts and close the Webex bridge. Also, close the Status Page incident and update the resolution (if not done in the previous step).
- [ ] **RCA & Postmortem** - Scribe needs create an initial [RCA and Postmortem](https://github.com/ncr-bsp/rca/new/master/postmortems) and close out with the help of the SMEs. Create a new PR for these new documents.
- [ ] Once **RCA** is known, we adjust error budgets of applications to reflect accurate numbers.
- [ ] Adjust any of the reported uptimes in StatusPage and PagerDuty if needed.
- [ ] Close this Github issue.
