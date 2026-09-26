# week 4
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

