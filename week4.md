[Home](index.md) | [Projects](projects.md) | [Resume](resume.md) | [Spiritual & Professional Growth](week4.md) | [Weekly Report](weekly-report.md) | [Spiritual Progression Portfolio](spiritual-portfolio.md)

# Quiet-Place Reflection: Agency, Diligence, and Growth

Reflecting on all the scriptures, conferences and speeches, one thing is clear: God does not intend for us to be passive observers waiting for detailed instructions before we act. Moral agency is an active power placed within us. Therefore, we are expected to take fruitful steps at taking initiative, not waiting for directions or commands from others on what we need to do.

In the IT space, there are opportunities to look, study and determine ways in which systems can be improved. Professionals must be proactive and not reactive. Also, as followers of Christ, we must balance our spirituality with our profession. Taking time to study and ponder about all that Jesus Christ is and the love of the Heavenly Father is a great execution of our agency.

# Documented Reflections on My Development Journey

## Moving from Passive Expectation to Consecrated Initiative

Early in any major undertaking, the natural human tendency is to seek step-by-step checklists or wait for explicit commands before taking initiative.

Pondering D&C 58:26–28 brought clarity to my career pivot from a bachelor's in the humanities into enterprise systems engineering.

- That transition succeeded because I chose not to wait to be compelled. It required taking the initiative to study late into the night, work through complex documentation and build practical lab architectures independently.
- In cloud infrastructure and Site Reliability Engineering, an engineer who only fixes what is explicitly assigned is merely reacting. True stewardship means actively identifying operational bottlenecks, automating fragile manual processes before they break and anticipating security risks of one's own free will.

## Agency as Creative Stewardship

In cloud computing, we provision infrastructure from code with Terraform, define state machines and organize container clusters with Kubernetes.

This technical stewardship mirrors the creative pattern of agency: taking unformed resources and structuring them into resilient, orderly environments where people and businesses can thrive.

## Overcoming Fear and Anxiety Through Anxious Engagement

Anxiety often stems from waiting passively under the weight of the unknown.

Meditating on verse D&C 58:28, "the power is in them, wherein they are agents unto themselves", clarified that action is the divine antidote to fear.

When I begin each morning with prayer and scripture study, anxiety is replaced with mental clarity and purpose. Taking deliberate action, doing my part through research, testing and methodically troubleshooting, allows the Spirit to direct my path and bless the outcome.

# Host-Based Intrusion Detection & Compliance Monitoring (Wazuh SIEM)

- **Technical Overview:** Deployed and configured the Wazuh open-source security platform in a Windows and Ubuntu VM to establish real-time host-based intrusion detection (HIDS), file integrity monitoring (FIM), and centralized security log analysis. Created custom detection rules to intercept privilege-escalation attempts and monitored critical system configuration files for unauthorized tampering.

- **Technical Skills Demonstrated:** Wazuh agent/manager architecture, File Integrity Monitoring (FIM), log analysis, custom XML decoders/rules, Linux system auditing and MITRE ATT&CK framework.

- **Spiritual & Character Reflection (Integrity in Hidden Places):** Host-based intrusion detection focuses on observing what happens inside a system when external perimeter defenses are cleared.

This project operationalizes the principle of Integrity in Hidden Places (1 Chronicles 29:17; Alma 27:27). File Integrity Monitoring tracks every silent change made to restricted files, mirroring how God examines the hidden intents of the heart.

Constructing transparent, vigilant monitoring systems serves as a protective stewardship: safeguarding system stability, honoring the agency of end users (2 Nephi 2:16, 27) and ensuring computing environments remain trustworthy and secure against undetected compromise.

# Ethical Dilemma: Essential Principles, Alternative Approach & Evaluation

## Essential Ethical Principles

- **Honesty:** The engineer showed complete transparency about system state and operational errors without evasion or half-truths.

- **Responsibility:** The engineer owned the consequences of her/his actions, protecting data stewardship and acting decisively to mitigate harm to stakeholders.

- **Fairness:** The engineer honored the trust of clients and team members whose operations depend on operational integrity, refusing to keep them uninformed of existential risks.

## Alternative Handling of the Dilemma: Coordinated Emergency Escalation & Containment Protocol

In the original response, the engineer self-reported directly to the Infrastructure Director after 30 minutes. While the eventual decision to report was ethical, an alternative and more structured approach focuses on immediate operational containment combined with transparent disclosure:

- **Immediate Freeze & Alert (0–5 Minutes):** The engineer immediately checks and suspends all automated backup disk writes, purges, and maintenance cron jobs on the target volume to maximize the chances of unallocated block recovery, while declaring a Sev-1 data-resiliency anomaly internal incident ticket.

- **Transparent, Multi-Party Disclosure (Within 15 Minutes):** Instead of an ad-hoc private meeting with leadership driven by individual panic, the engineer invokes the formal incident response protocol, notifying the Infrastructure Director, the lead Database Administrator, and the Security/Compliance Officer simultaneously with a factual timeline, the exact command run and the known scope of deleted snapshot ranges.

- **Collaborative Recovery & Blameless Post-Mortem:** The engineer leads the data recovery effort alongside storage vendors and DBAs to restore point-in-time cold snapshots, followed by publishing an open blameless post-mortem detailing engineering controls and policies: mandatory `--dry-run` checks, automated snapshot locks and multi-party signoffs for data-destruction commands.

## Evaluation of Outcomes for Stakeholders

- **For the Clients & End Users:** Maximizes data recovery chances by freezing disk writes within minutes rather than letting background services potentially overwrite unallocated blocks during the 30-minute hesitation window, drastically reducing exposure to unrecoverable data loss.

- **For the Engineering Team:** Elevates incident response from an emotional personnel issue to an objective engineering event; prevents duplicate or conflicting troubleshooting efforts by establishing immediate cross-team visibility across DBAs and operations.

- **For Leadership & Management:** Provides immediate, verifiable visibility required to assess contractual Service Level Agreements (SLAs) and regulatory reporting requirements accurately, eliminating legal exposure stemming from delayed notification.

- **For the Engineer:** Replaces personal anxiety and self-protective panic with immediate, professional accountability; demonstrates disciple-leadership by prioritizing system recovery and stakeholder welfare over fear of disciplinary consequences.

## This report records the changes I have made in my SIEM for intrusion detection installation project and the challenges they addressed including ethical considerations.

## Improvements and Challenges.

### Hardening & Identity Management

- **Challenge:** The Wazuh components(agents and dashboard manager) use default credentials so there is risk of exposure in case of an attack.
- **Refinement:** I replaced default passwords with secure passwords and saved them in a keystore.

### High Availability Dashboard Architecture

- **Challenge:** In the original design, if the single OVA node halted or experienced indexer restart delays, analyst visibility was completely lost
- **Refinement:** Added a second dashboard node and HAProxy load balancing with SSL termination and session persistence. Both dashboards connect to clustered Indexer and Manager nodes.

### Coordinated Update Lifecycle

- **Challenge:** Updating agents before the manager can cause compatibility and telemetry issues.
- **Refinement:** Adopted a Manager-First, Agent-Second process, automated configuration backups and used agent_upgrade for rolling endpoint updates.

### Integration of Ethical Considerations

Emphasis was placed on data sanitization to improve accessibility while also improving data privacy.

- **Logs sanitization:** Added masking rules to prevent accidentally entered passwords from being stored in SIEM logs.
- **Proportional Monitoring:** Limited monitoring to security events, system anomalies, and service logs while excluding personal user data.
- **Data Retention:** Applied lifecycle policies to archive and delete telemetry after required audit periods.

While examining the project I was able to pinpoint the limitations by placing myself in the place of the user and the organization the SIEM protects. I was able to determine the improvements by approaching them from reliability, security and operational markers.

I believe these refinements would tighten the security surrounding data storage, user accessibility and infrastructure reliability.


## Peer review for Rolando Alfaro Rominez.

I think this is a great project, especially with the refinements you have included.

It highlights the importance of documentation in a technical organization especially for tasks that are repeatable. This improves the accessibility of information by team members or volunteers, increasing the efficiency in configuring and delivering systems.

The implementation of cross-platform tools like BitRazer to solve the same problem across Windows, Mac and Ubuntu Operating Systems shows resourcefulness and establishes your expertise as a refined technologist. It also saves the time of fellow team members, as they can focus on mastering one tool for that task.

The consideration for orderliness by recommending a color-management scheme for PCs is a great way to improve efficiency. Also, the introduction of a standard for processes also helps the team member in aligning their goals and understanding what is expected of them. I believe this is an act that increases accountability and morality in the workspace.

The decision to protect customer’s personal data from team members is a great way to ensure that everyone is compliant with data protection laws and the moral code expected as disciples of Jesus Christ.

Overall, I think this was a well-executed project, I wish you the best in your endeavors.


## Submitted by Feyisayo Famakinde

## Abstract

Intrusion detection systems are guardrails for a network; they detect
issues within systems and report them as alerts. Security Information
Event Management(SIEM) systems often come with these agents, one of the
many SIEM’s available is called Wazuh. This document would provide
information on the installation and configuration of its agents and
console.


## Registering an Intrusion detection Agent with a Security Information Event Management Solution.

## EXECUTIVE SUMMARY

## Overview - The Quick Pitch

This summary will demonstrate how Wazuh agents collect information about
every activity within a particular operating system after deployment and
configuration. The information collected would also be displayed in a
Graphical User Interface where data can be analyzed and alerts verified.

## The Solution

## Installation.

For this solution, I will be working with three Virtual Machines in
VirtualBox: two Windows Server VM and Ubuntu Server VM. For the Wazuh
Dashboard, I installed an OVA file; an already packaged image that has
all the necessary packages to run the Wazuh Solution in Virtual box on
both windows machines.

Also, to ensure all my Virtual Machines can communicate with each other
and the internet, I attached both a NAT adapter and Host Only adapter.
The NAT adapter makes connections to the internet possible while the
Host Only adapter makes connections within the VMs possible. Starting up
the Wazuh server, authenticating with the default username and password
then I tried to access the dashboard from my Windows Server since it was
the only machine with a GUI on my list. I had a bit of challenge
accessing it from my browser because I inputted “http” instead of
“https” I got an error because the dashboard/server listens on port 443.
I was able to find that out after accessing the dashboard config file, I
was able to retrieve the appropriate IP address by using the “ip a”
command within the Wazuh server. VirtualBox host network is within the
192.168.56.0/24 network, so I knew to look for IP addresses within that
range.

**Configuration.**

After authenticating into the dashboard, it was time to deploy agents to
my Windows and Ubuntu servers. Selecting the appropriate OS, including
the server’s IP address then copying the commands provided in the deploy
agent interface. Running commands in the appropriate machines installs
the wazuh agents on each machine, for configuration I ran into some
issues with the agents not recognizing the wazuh manager IP.

For Windows, after installation a prompt comes up with a box for the
manager IP, inputting Wazuh’s server IP address for the Virtual Box host
only Network Interface is the correct value here.

For Ubuntu, although the command for installation has the variable
configured for some reason probably due to shell complexities, the value
is not configured. I had to do this manually at
<span class="mark">/var/ossec/etc/ossec.conf</span> which is the
configuration file for the agent.

Once everything is configured properly and the services are restarted,
the agents should show up as active on the dashboard. I was able to
access the agents by clicking on the agents’ button, scrolling down then
selecting any of the agents I need information on.

Clicking on any of these agents takes you to a dashboard with widgets
that contain event counts, evaluation based on the MITRE attack
framework and a Vulnerability detection widget. Clicking on any of the
widgets takes you to a larger dashboard with more details.

**Network Issues.**

I didn’t encounter lots of networking issues but one major error I
encountered was starting up the Wazuh agent after booting it back up.
There were times when I needed to access the dashboard, but I got a
blank screen, the API wasn’t available at times but after doing my
research I was able to resolve these issues.

To troubleshoot, I had to look at the logs first, the command
<span class="mark">“tail -n 50 /var/ossec/logs/api.log”</span> shows the
reason the API might be failing. From there I discovered that the
wazuh-db service was not running. After some research online, I was able
to resolve the issue by restarting the wazuh-indexer which contains all
the services needed by the wazuh manager. The command used was “sudo
/var/ossec/bin/wazuh-control restart” this reloads all the packages and
daemons responsible for the successful initialization of the wazuh API
and dashboard. Then check the status with <span class="mark">“sudo
/var/ossec/bin/wazuh-control status”</span> to confirm availability.

For the dashboard, I checked the status with <span class="mark">“sudo
service wazuh-dashboard status”</span> confirmed it was in a failed
state then restarted with <span class="mark">“sudo service
wazuh-dashboard restart”</span>.

**Report Summary.**

- **Date Range:** June 17 – June 18, 2025

- **System Monitored:** Ubuntu 24:04, Windows Server 2022

- **IDS Tool:** Wazuh

During the monitoring period from June 17 to June 18, Wazuh detected 40
authentication failures on the Ubuntu server and 184 authentication
failures on the Window Server. Brute-force attacks through SSHd and an
unknown user.

Here is a link to the report on the events

**[Wazuh
Events](https://docs.google.com/spreadsheets/d/1N3nWmtObIrcrJZr7EJcO4ZbJhws4au-v/edit?usp=sharing&ouid=114825843182011719877&rtpof=true&sd=true)
(Please press CTRL + click to access link)**

**Identified Baseline Deficiencies**

- Insecure Credential Posture: The initial deployment relied on default
  system-level credentials (wazuh-user / wazuh) and unrotated web
  console credentials (admin / admin).

- Dashboard Availability Vulnerabilities: Running the presentation tier
  directly on the resource-constrained all-in-one appliance led to API
  handshake failures (HTTP 500 / Error 3002) and "Wazuh dashboard server
  is not ready yet" service crashes caused by underlying wazuh-db
  process drops.

- Unstructured Upgrade Workflows: Agent enrollment relied on manual
  agent-side IP input, with no automated lifecycle management, rolling
  update plans, or version-pinning strategies.

- Privacy Ingestion Gaps: Raw auth failure logs ingested unmasked string
  tokens, exposing passwords in username fields to all dashboard
  operators.

- Accessibility Limitations: Operational dashboards relied entirely on
  monochromatic red/green status markers, offering no semantic structure
  or screen-reader accommodations for security analysts

**Technical Enhancements & Reliability Engineering**

- Credential Hardening & Identity Management: Because Wazuh shares
  internal state tokens across the manager API, OpenSearch indexer and
  dashboard layers, credentials must be rotated across the operating
  system.

- Multi-Instance High-Availability (HA) Dashboard Design: The Wazuh
  Dashboard is an asynchronous, stateless interface querying the Wazuh
  Indexer on port 9200 and the Wazuh Manager API on port 55000. Running
  multiple redundant instances behind a load balancer removes single
  points of failure.

- Coordinated Update & Upgrade Lifecycle: To protect against system
  failure errors, the upgrade of the indexer, agent and dashboard needs
  to be orchestrated in phases. Upgrades are done remotes through the
  built-in upgrade manager via the manager’s console

- Data privacy and protection: Custom log decoders are deployed on the
  ingestion layer to sanitize authentication strings prior to indexing.
  Log data was configured to be purged after 90 days.

- Multi-Modal Visual Signifiers**:** The default Wazuh UI communicates
  status almost exclusively through color-coded rings and dots (e.g.,
  green for active, red for critical vulnerabilities). The refined
  configuration included texts such as ACTIVE, WARN, OFFLINE with
  color-codes for user accessibility.

## Conclusion.

From the summary above, Wazuh provides stellar detection solutions when
properly configured. We can conclude by acknowledging that Intrusion
Detection Systems are vital to the health of a network because they
provide information on events that happen within the network. With this
information, security teams are aware of potential attacks on the
organization’s assets and what to do to ensure solid protection of the
network.

Also, refining a SIEM implementation requires moving beyond simple
connectivity and agent enrollment. By pairing high-availability
architecture and structured update lifecycles with robust credential
hygiene, log sanitization and accessible dashboard design. The Wazuh
deployment evolves from a vulnerable single-node lab into a resilient
and enterprise-ready monitoring platform that balances robust security
with ethical responsibility.

