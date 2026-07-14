# 🎯 Module 15 – INTRODUCTION TO RED TEAM PLAN AND EXECUTION
<br>

> [!NOTE]
> **Module Overview:** This module transitions from standard penetration testing into Red Teaming. It covers the fundamental frameworks used to model advanced persistent threats (APTs), including the Cyber Kill Chain and MITRE ATT&CK, as well as the lifecycle and execution phases of a Red Team engagement.

---

## ⛓️ 1. The Cyber Kill Chain

Developed by Lockheed Martin, the Cyber Kill Chain framework models the stages of a cyberattack. Breaking the chain at any point disrupts the attack.

<details>
<summary><b>🔍 Expand to view the Cyber Kill Chain Model</b></summary>
<br>

```mermaid
graph TD
    A[Reconnaissance<br><i>Harvesting email addresses, OSINT</i>] --> B[Weaponization<br><i>Coupling exploit with backdoor</i>]
    B --> C[Delivery<br><i>Email, Web, USB</i>]
    C --> D[Exploitation<br><i>Executing code on victim system</i>]
    D --> E[Installation<br><i>Installing malware/backdoors</i>]
    E --> F[Command & Control C2<br><i>Establishing remote control</i>]
    F --> G[Actions on Objectives<br><i>Data exfiltration, encryption, destruction</i>]

    style A fill:#2d3748,stroke:#4a5568,color:#fff
    style B fill:#3182ce,stroke:#2b6cb0,color:#fff
    style C fill:#d69e2e,stroke:#b7791f,color:#fff
    style D fill:#e53e3e,stroke:#c53030,color:#fff
    style E fill:#805ad5,stroke:#6b46c1,color:#fff
    style F fill:#d53f8c,stroke:#b83280,color:#fff
    style G fill:#e53e3e,stroke:#c53030,color:#fff,stroke-width:4px
```
</details>

### Defensive Action Matrix
| Kill Chain Phase | Defensive Action (Example) |
| :--- | :--- |
| **Reconnaissance** | Web analytics monitoring, Firewall logs |
| **Weaponization** | N/A (Happens on attacker's infrastructure) |
| **Delivery** | Proxy filters, Antivirus, Email Security Gateways |
| **Exploitation** | Patch management, Exploit Mitigation (DEP/ASLR) |
| **Installation** | EDR (Endpoint Detection and Response), HIPS |
| **Command & Control** | DNS filtering, Network segmentation, NIDS |
| **Actions on Objectives** | DLP (Data Loss Prevention), Incident Response |

---

## 🧩 2. MITRE ATT&CK Framework

While the Cyber Kill Chain models the *flow* of an attack, the MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) framework provides a globally accessible knowledge base of adversary *tactics and techniques* based on real-world observations.

### Tactics vs. Techniques
*   **Tactics (The "Why"):** The adversary's technical goal (e.g., Initial Access, Persistence).
*   **Techniques (The "How"):** How the adversary achieves the tactical goal (e.g., Phishing, Registry Run Keys).
*   **Procedures:** The specific, highly detailed implementation (e.g., APT29 using a specific PowerShell script).

<details>
<summary><b>📊 Core ATT&CK Tactics Overview</b></summary>
<br>

```mermaid
mindmap
  root((MITRE ATT&CK))
    Initial Access
      Phishing
      Exploit Public-Facing App
    Execution
      Command and Scripting Interpreter
      WMI
    Persistence
      Boot or Logon Autostart Execution
      Scheduled Task/Job
    Privilege Escalation
      Process Injection
      Exploitation for Privilege Escalation
    Defense Evasion
      Obfuscated Files or Information
      Modify Registry
    Credential Access
      OS Credential Dumping
      Brute Force
```
</details>

---

## ⚔️ 3. Red Team Phases and Cycle

A Red Team engagement is fundamentally different from a Penetration Test. While a Pentest aims to find *as many vulnerabilities as possible* in a given scope, a Red Team engagement aims to assess the organization's **detection and response capabilities** (the Blue Team) by emulating a real-world threat actor.

### Red Team Lifecycle

```mermaid
journey
    title Red Team Engagement Lifecycle
    section Planning
      Rules of Engagement (RoE): 5: Red Team, Client
      Threat Intelligence & Scoping: 4: Red Team
    section Execution
      Infrastructure Setup (C2, Phishing Domains): 3: Red Team
      Initial Compromise: 4: Red Team
      Persistence & Lateral Movement: 5: Red Team
      Actions on Objectives: 5: Red Team
    section Culmination
      Reporting & Remediation: 4: Red Team, Blue Team
      Purple Teaming (Collaborative Review): 5: Red Team, Blue Team
```

> [!TIP]
> **OPSEC (Operational Security):** During a Red Team engagement, avoiding detection is paramount. Attackers (and Red Teamers) use proxies, redirectors, and carefully crafted payloads to bypass EDR/SIEM solutions.

---

## 🔬 4. TryHackMe Research Rooms

To further your understanding of Red Teaming concepts, complete the following practical research rooms:

1.  **Red Team Fundamentals:** [https://tryhackme.com/room/redteamfundamentals](https://tryhackme.com/room/redteamfundamentals)
    *   *Focus:* Differences between Red, Blue, and Purple teams; Introduction to OPSEC.
2.  **Red Team Engagements:** [https://tryhackme.com/room/redteamengagements](https://tryhackme.com/room/redteamengagements)
    *   *Focus:* Scoping, Rules of Engagement (RoE), defining objectives, and reporting.

---

## ⚖️ 5. Red Teaming vs. Penetration Testing Phases

It is critical to understand the difference between standard PT phases and Red Teaming phases.

| Feature | Penetration Testing | Red Teaming |
| :--- | :--- | :--- |
| **Primary Goal** | Find as many vulnerabilities as possible. | Test the organization's detection & response (Blue Team). |
| **Scope** | Usually restricted to specific apps/networks. | Often wide-open ("Assume Breach", physical, social engineering). |
| **Stealth (OPSEC)**| Low priority. Scanners (Nmap, Nessus) are loud. | High priority. Must emulate APT stealth techniques. |
| **Duration** | 1 to 3 weeks. | 1 to 3 months (or longer). |
| **Deliverable** | Vulnerability report and remediation steps. | Attack narrative, timeline, and Blue Team detection analysis. |

<br>
<p align="center"><i>End of Module 15</i></p>
