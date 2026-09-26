[Home](index.md) | [Week 1](#week-1) | [Week 2](#week-2) | [Week 3](#week-3) | [Week 4](#week-4) | [View_Refined_Project](Security Information Event Management System_Refined.md) |
 [View_IT_Refinement_report](IT 497 Refinement report.md) | [View_Peer_review_Evaluation](Peer review evaluation for Rolando Alfaro Ramirez.md)


# This report records the changes I have made in my SIEM for intrusion detection installation project and the challenges they addressed including ethical considerations.

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
