<p align="center">
  <img src="https://i.imgur.com/u9C8Cbv.gif" alt="Fsociety Banner"/>
</p>

<p align="center">
<pre>
<font color="#00ADEF">███████╗</font><font color="#FFFFFF">███████╗ ██████╗  ██████╗██╗███████╗████████╗██╗   ██╗</font>
<font color="#00ADEF">██╔════╝</font><font color="#FFFFFF">██╔════╝██╔═══██╗██╔════╝██║██╔════╝╚══██╔══╝╚██╗ ██╔╝</font>
<font color="#00ADEF">█████╗  </font><font color="#FFFFFF">███████╗██║   ██║██║     ██║█████╗     ██║    ╚████╔╝ </font>
<font color="#00ADEF">██╔══╝  </font><font color="#FFFFFF">╚════██║██║   ██║██║     ██║██╔══╝     ██║     ╚██╔╝  </font>
<font color="#00ADEF">██║     </font><font color="#FFFFFF">███████║╚██████╔╝╚██████╗██║███████╗   ██║      ██║   </font>
<font color="#00ADEF">╚═╝     </font><font color="#FFFFFF">╚══════╝ ╚═════╝  ╚═════╝╚═╝╚══════╝   ╚═╝      ╚═╝   </font>
</pre>
</p>

<div align="center">

# <samp>Playbook: AD_Liquidation</samp>
**<samp>Surgical Active Directory Annihilation | From Patient Zero to Domain Dominance</samp>**

<br>

<samp>Architect: <a href="https://github.com/fsoc-ghost-0x">C0deGhost</a> | Status: <font color="#00ff00">ACTIVE</font> | Classification: <font color="#FF4646">DOMAIN_ADMIN_RESTRICTED</font></samp>

<br><br>

<img src="https://img.shields.io/badge/Target-Active_Directory-0078D6?style=for-the-badge&logo=windows" alt="Target"/>
<img src="https://img.shields.io/badge/Agent-SPECTRE__V5-00ADEF?style=for-the-badge&logo=ghost" alt="Agent"/>
<img src="https://img.shields.io/badge/Impact-Total_Takeover-FF4646?style=for-the-badge&logo=target" alt="Impact"/>

</div>

<br>

> **[ DIRECTIVE LOG ]**
> **Purpose:** Standardize the execution flow for obliterating Active Directory environments. 
> **Scope:** Applied when the initial foothold (Patient Zero) is established inside a Windows Domain environment.

<br>

## <samp>▌ <u>0x01_THE_TRUST_GRAPH (PHILOSOPHY)</u></samp>

<samp>
Active Directory is not a network; it is a macroscopic graph of misconfigured trust. 
<br><br>
In this playbook, we do not rely on brute-force or noisy exploits. We rely on the mathematical exploitation of Kerberos, identity delegation, and Certificate Services (AD CS). The objective is to identify the shortest, most silent path between an unprivileged user and the Domain Controller, manipulating Access Control Lists (ACLs) to make the domain hand us the keys to the kingdom voluntarily.
</samp>

<br>

## <samp>▌ <u>0x02_EXECUTION_PHASES (THE ANNIHILATION PATH)</u></samp>

| <samp>Phase</samp> | <samp>Tactical Objective</samp> | <samp>Execution Methodology</samp> |
| :--- | :--- | :--- |
| <samp><b>1. Deep Graph Enumeration</b></samp> | <samp>Map the Trust Maze</samp> | <samp>Execution of BloodHound/SharpHound entirely in memory (LoTL). Extraction of LDAP queries, ACE/DACL mapping, and identification of vulnerable Certificate Templates.</samp> |
| <samp><b>2. Identity Forging</b></samp> | <samp>Seize Lateral Credentials</samp> | <samp>AS-REP Roasting, Kerberoasting (TGS extraction), and targeted NTLM Relaying (Coercing machine accounts via PetitPotam/Shadow Credentials).</samp> |
| <samp><b>3. Vertical Subversion</b></samp> | <samp>Exploit Misconfigurations</samp> | <samp>Exploitation of AD CS (ESC1 through ESC16). Forging User Principal Names (UPN) to request Domain Admin certificates, bypassing standard authentication entirely.</samp> |
| <samp><b>4. Silent Pivoting</b></samp> | <samp>Cross-Boundary Movement</samp> | <samp>Pass-The-Ticket (PTT) and Over-Pass-The-Hash. Utilization of WinRM and WMI for fileless lateral movement. No RDP. No noisy GUI interactions.</samp> |
| <samp><b>5. Domain Liquidation</b></samp> | <samp>Total Domain Dominance</samp> | <samp>DCSync attack to extract the <code>NTDS.dit</code> database. Forging a Golden Ticket (krbtgt) for 10-year immutable persistence.</samp> |

<br>

## <samp>▌ <u>0x03_THE_TACTICAL_ARSENAL</u></samp>

<samp>Standard open-source tools are heavily monitored by EDRs. Execution of this playbook mandates the use of FSOCIETY's customized, obfuscated variants stored within <code>Alderson_Core</code>:</samp>

*   **Custom Rubeus:** Compiled with stripped signatures and Direct Syscalls for stealth ticket manipulation.
*   **Certify/Certipy (Modified):** For auditing and exploiting AD CS infrastructure without triggering Event ID 4898.
*   **ShadowCreds Injector:** Custom C# tooling for Resource-Based Constrained Delegation (RBCD) attacks.
*   **In-Memory Mimikatz:** Executed exclusively via reflective DLL injection or custom process hollowing to bypass LSASS credential guard.

<br>

## <samp>▌ <u>0x04_ATTACK_FLOW (THE KILL-CHAIN)</u></samp>

<samp>Visual representation of the AD Liquidation process:</samp>

```mermaid
graph TD;
    ZERO["<b>Patient Zero</b><br>(Low Priv User)"] --> ENUM["<b>LDAP/Graph Enumeration</b><br>(BloodHound/Certify)"];
    ENUM --> VULN{"<b>Vulnerability Identified</b>"};
    
    VULN -- "Vulnerable Certificate" --> ADCS["<b>AD CS Exploitation</b><br>(ESC1/ESC8)"];
    VULN -- "Weak ACL / Delegation" --> RBCD["<b>RBCD / Shadow Credentials</b>"];
    VULN -- "Service Accounts" --> ROAST["<b>Kerberoasting</b>"];

    ADCS --> TICKET["<b>Forge Silver/Golden Ticket</b><br>(Pass-The-Ticket)"];
    RBCD --> TICKET;
    ROAST --> TICKET;

    TICKET --> DC["<b>Domain Controller Compromise</b><br>(DCSync / NTDS.dit)"];
    DC --> PERSIST["<b>Absolute Persistence</b><br>(Skeleton Key / Golden Ticket)"];

    style ZERO fill:#111,stroke:#666,stroke-width:1px,color:#aaa
    style ENUM fill:#111,stroke:#00adef,stroke-width:2px,color:#fff
    style VULN fill:#111,stroke:#f5ba14,stroke-width:2px,color:#fff
    style ADCS fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style RBCD fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style ROAST fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style TICKET fill:#111,stroke:#ff8c00,stroke-width:2px,color:#fff
    style DC fill:#111,stroke:#00ff00,stroke-width:3px,color:#00ff00
    style PERSIST fill:#111,stroke:#00adef,stroke-width:2px,color:#fff
```

<br>

## <samp>▌ <u>0x05_PROJECT_ARCHON_INTEGRATION (SPECTRE)</u></samp>

<div style="border-left: 4px solid #00ADEF; padding-left: 15px; background: rgba(0, 173, 239, 0.05); padding: 15px;">
<samp>
This playbook serves as the primary execution logic for <b>[+] SPECTRE_V5</b>.
<br><br>
When the NEXUS is deployed into a Windows Domain, SPECTRE ingests this document to autonomously map the trust graph. It teaches the AI to prioritize cryptographic attacks (Kerberos/Certificates) over noisy memory corruption exploits, ensuring the automated liquidation of the Active Directory remains forensically invisible.
</samp>
</div>

<br>

<div align="center">
<hr style="width: 80%; border: 1px solid #333;">
<br>
<samp><strong><font color="#00ADEF">WE ARE FSOCIETY. WE ARE FINALLY FREE. WE ARE FINALLY AWAKE.</font></strong></samp>
</div>
