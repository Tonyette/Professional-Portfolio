[Home](index.md) | [Week 1](#week-1) | [Week 2](#week-2) | [Week 3](#week-3) | [Week 4](#week-4) | [View Refined Project](Security Information Event Management System_Refined.md) | [View IT Refinement report](IT 497 Refinement report.md) | [View Peer review Evaluation](Peer review evaluation for Rolando Alfaro Rominez.md)


Submitted by

Feyisayo Famakinde

# Abstract

Intrusion detection systems are guardrails for a network; they detect
issues within systems and report them as alerts. Security Information
Event Management(SIEM) systems often come with these agents, one of the
many SIEM’s available is called Wazuh. This document would provide
information on the installation and configuration of its agents and
console.


# Registering an Intrusion detection Agent with a Security Information Event Management Solution.

# EXECUTIVE SUMMARY

# Overview - The Quick Pitch

This summary will demonstrate how Wazuh agents collect information about
every activity within a particular operating system after deployment and
configuration. The information collected would also be displayed in a
Graphical User Interface where data can be analyzed and alerts verified.

# The Solution

# Installation.

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

# Conclusion.

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

#  Refinement Section

**This report records the changes I have made in my SIEM for intrusion
detection installation project and the challenges they addressed
including ethical considerations.**

## Improvements and Challenges.

**Hardening & Identity Management**

- **Challenge:** The Wazuh components(agents and dashboard manager) use
  default credentials so there is risk of exposure in case of an attack.

- **Refinement:** I replaced default passwords with secure passwords and
  saved them in a keystore.

**High Availability Dashboard Architecture**

- **Challenge:** In the original design, if the single OVA node halted
  or experienced indexer restart delays, analyst visibility was
  completely lost

- **Refinement:** Added a second dashboard node and HAProxy load
  balancing with SSL termination and session persistence. Both
  dashboards connect to clustered Indexer and Manager nodes.

**Coordinated Update Lifecycle**

- **Challenge:** Updating agents before the manager can cause
  compatibility and telemetry issues.

- **Refinement:** Adopted a Manager-First, Agent-Second process,
  automated configuration backups and used agent_upgrade for rolling
  endpoint updates.

## Integration of Ethical Considerations

Emphasis was placed on data sanitization to improve accessibility while
also improving data privacy.

- **Logs sanitization:** Added masking rules to prevent accidentally
  entered passwords from being stored in SIEM logs.

- **Proportional Monitoring:** Limited monitoring to security events,
  system anomalies, and service logs while excluding personal user data.

- **Data Retention:** Applied lifecycle policies to archive and delete
  telemetry after required audit periods.

While examining the project I was able to pinpoint the limitations by
placing myself in the place of the user and the organization the SIEM
protects. I was able to determine the improvements by approaching them
from reliability, security and operational markers.

I believe these refinements would tighten the security surrounding data
storage, user accessibility and infrastructure reliability.
