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

# <samp>Node_0x05: Tactical_Doctrine_&_Playbooks</samp>
**<samp>Standard Operating Procedures | MITRE ATT&CK Mappings | Intrusion Methodology</samp>**

<br>

<samp>Architect: <a href="https://github.com/fsoc-ghost-0x">C0deGhost</a> | Status: <font color="#00ff00">ACTIVE</font> | Classification: <font color="#00ADEF">APT_DOCTRINE</font></samp>

</div>

<br>

<div align="center">
  <img src="https://img.shields.io/badge/Intel-SOPs_&_Playbooks-00ADEF?style=for-the-badge&logo=bookstack" alt="Playbooks"/>
  <img src="https://img.shields.io/badge/Doctrine-Military_Grade-660000?style=for-the-badge&logo=arch-linux" alt="Doctrine"/>
  <img src="https://img.shields.io/badge/Framework-MITRE_ATT&CK-black?style=for-the-badge&logo=mitre" alt="MITRE"/>
</div>

<br><br>

## <samp>▌ <u>0x01_THE_PHILOSOPHY_OF_THE_PLAYBOOK</u></samp>

<div style="border-left: 4px solid #00ADEF; padding-left: 15px; background: rgba(0, 173, 239, 0.05); padding: 15px;">
<samp>
A hacker without a methodology is merely a vandal. <b>FSOCIETY is an institution.</b>
<br><br>
This node houses the intellectual core of our intrusion operations. We do not rely on improvisation; we rely on <b>Standard Operating Procedures (SOPs)</b> and deterministic execution. The documents contained within this sector outline the exact steps, OPSEC protocols, and tactical playbooks required to transform a locked infrastructure into a fully compromised domain.
<br><br>
Here, chaos is standardized. Every zero-day fired and every Lateral Movement executed in the field originates from the doctrines established in this vault.
</samp>
</div>

<br>

## <samp>▌ <u>0x02_TACTICAL_DIRECTORY_TREE</u></samp>

<samp>The internal structure of the Doctrine Node. Navigate to specific sub-directories for detailed execution methodologies:</samp>

```text
05_TACTICAL_DOCTRINE_&_PLAYBOOKS/
├── 01_FSOCIETY_METHODOLOGY_BLUEPRINT/   # The 5-Phase Master Kill-Chain
│   └── README.md                        # (Recon -> Access -> Exploit -> Post -> Plunder)
│
├── 02_OPSEC_&_STEALTH_PROTOCOLS/        # Rules of Engagement for invisibility
│   └── Anti_Forensics_Guidelines.md     # Timestomping, Log wiping, RAM-only execution
│
├── 03_MITRE_ATTACK_MAPPINGS/            # Translation of our custom TTPs to industry standards
│   └── Enterprise_Matrix_Coverage.md    # Mapping Fsociety payloads to MITRE IDs
│
└── 04_TARGET_SPECIFIC_PLAYBOOKS/        # Surgical playbooks for distinct environments
    ├── AD_Liquidation_Playbook.md       # From unprivileged user to Domain Admin
    ├── Cloud_IAM_Subversion.md          # AWS/Azure/GCP specific attack paths
    └── ICS_SCADA_Infiltration.md        # Protocols for air-gapped & physical systems
```

<br>

## <samp>▌ <u>0x03_RULES_OF_ENGAGEMENT (RoE)</u></samp>

<samp>All FSOCIETY operations documented in <code>Fsociety_Operations_Logs.dat</code> strictly adhere to the following baseline directives:</samp>

<table width="100%" style="border-collapse: collapse; border: 1px solid #333; background: transparent;">
  <tr>
    <td width="20%" style="padding: 15px; border: 1px solid #333; background: rgba(0, 173, 239, 0.05);">
      <samp><font color="#00ADEF"><b>DIRECTIVE 01</b></font></samp>
    </td>
    <td style="padding: 15px; border: 1px solid #333;">
      <samp><b>Absolute Isolation (Zero-Trust Origin):</b> No payloads are to be compiled, staged, or fired from non-volatile or attributable hardware. Operations must route through hardened Tor/I2P circuits or disposable VPS relays.</samp>
    </td>
  </tr>
  <tr>
    <td width="20%" style="padding: 15px; border: 1px solid #333; background: rgba(0, 173, 239, 0.05);">
      <samp><font color="#00ADEF"><b>DIRECTIVE 02</b></font></samp>
    </td>
    <td style="padding: 15px; border: 1px solid #333;">
      <samp><b>Living off the Land (LoTL) Supremacy:</b> Native OS binaries (PowerShell, WMI, Bash, Cron) are always the primary weapon choice. Custom malware from <i>Alderson_Core</i> is deployed only when native tools are insufficient for the objective.</samp>
    </td>
  </tr>
  <tr>
    <td width="20%" style="padding: 15px; border: 1px solid #333; background: rgba(0, 173, 239, 0.05);">
      <samp><font color="#00ADEF"><b>DIRECTIVE 03</b></font></samp>
    </td>
    <td style="padding: 15px; border: 1px solid #333;">
      <samp><b>Failure Autopsy (The ELLIOT Protocol):</b> A blocked payload is not a failure; it is telemetry. Any payload caught by EDR must trigger an immediate OPSEC review and structural rewrite before re-engagement.</samp>
    </td>
  </tr>
</table>

<br>

## <samp>▌ <u>0x04_PROJECT_ARCHON_INTEGRATION</u></samp>

<samp>The doctrines housed in this node are the fundamental <b>Behavioral Rulesets</b> for our Autonomous AI.</samp>

<div style="background-color: #0a0a0a; border: 1px solid #333; border-left: 4px solid #00ff00; padding: 15px; border-radius: 5px;">
<samp>
When <b>ÆON_STRIKE</b> or any FSOCIETY_DEMONS_CORE (such as FENRIR or SPECTRE) executes a sub-routine, they do not guess. They cross-reference the target environment against the <code>TARGET_SPECIFIC_PLAYBOOKS</code> stored in this directory. This node teaches the AI <i>how to think like a Ghost</i>.
</samp>
</div>

<br>

<div align="center">
<hr style="width: 80%; border: 1px solid #333;">
<br>
<i><font color="#ff4500" face="monospace">"Control is an illusion. I am the exploit."</font></i><br><br>
<br><br>
<samp><strong><font color="#00ADEF">WE ARE FSOCIETY. WE ARE FINALLY FREE. WE ARE FINALLY AWAKE.</font></strong></samp>
</div>
