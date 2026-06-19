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

# <samp>Playbook: Cloud_IAM_Subversion</samp>
**<samp>Control Plane Annihilation | Cross-Tenant Pivoting | Absolute IAM Dominance</samp>**

<br>

<samp>Architect: <a href="https://github.com/fsoc-ghost-0x">C0deGhost</a> | Status: <font color="#00ff00">ACTIVE</font> | Classification: <font color="#FF4646">CLOUD_ROOT_RESTRICTED</font></samp>

<br><br>

<img src="https://img.shields.io/badge/Target-AWS%2FAzure%2FGCP-232F3E?style=for-the-badge&logo=amazon-aws" alt="Target"/>
<img src="https://img.shields.io/badge/Agent-ROMERO__V34-4682b4?style=for-the-badge&logo=ghost" alt="Agent"/>
<img src="https://img.shields.io/badge/Impact-Control_Plane_Seizure-FF4646?style=for-the-badge&logo=target" alt="Impact"/>

</div>

<br>

> **[ DIRECTIVE LOG ]**
> **Purpose:** Standardize the execution flow for collapsing Cloud Environments via Identity and Access Management (IAM) abuse.
> **Scope:** Applied when the target infrastructure resides in AWS, Azure (Entra ID), or GCP. Focuses entirely on the Control Plane rather than individual compute instances.

<br>

## <samp>▌ <u>0x01_THE_IDENTITY_PERIMETER (PHILOSOPHY)</u></samp>

<samp>
In the Cloud, there is no network perimeter; <b>Identity is the perimeter</b>. 
<br><br>
This playbook discards traditional network exploitation. We do not care about port scanning EC2 instances. We target the <b>Control Plane</b>. By exploiting Server-Side Request Forgery (SSRF) to extract ephemeral tokens, abusing over-permissive IAM roles, and forging federated identities (Golden SAML), we turn the cloud provider's own management APIs into our weapon. If we control the IAM, we control the reality of the infrastructure.
</samp>

<br>

## <samp>▌ <u>0x02_EXECUTION_PHASES (THE CLOUD ANNIHILATION PATH)</u></samp>

| <samp>Phase</samp> | <samp>Tactical Objective</samp> | <samp>Execution Methodology</samp> |
| :--- | :--- | :--- |
| <samp><b>1. Foothold & Metadata Extraction</b></samp> | <samp>Breach the Compute Layer</samp> | <samp>Exploitation of SSRF vulnerabilities on exposed web applications to query the Instance Metadata Service (IMDSv1/IMDSv2). Extraction of ephemeral <code>STS AssumeRole</code> credentials. Alternatively, extraction of hardcoded AWS/Azure keys from exposed GitHub repositories or misconfigured CI/CD pipelines.</samp> |
| <samp><b>2. Cloud Control Plane Enum</b></samp> | <samp>Map the IAM Graph</samp> | <samp>Deployment of automated reconnaissance via Cloud APIs. Auditing attached policies, identifying "Shadow Admins", and mapping excessive permissions (e.g., <code>iam:PassRole</code>, <code>iam:AttachUserPolicy</code> in AWS; Privileged Role Assignments in Azure).</samp> |
| <samp><b>3. Vertical IAM Escalation</b></samp> | <samp>Seize Administrative Power</samp> | <samp>Self-elevation of privileges by attaching Administrator policies to the compromised identity. Abuse of Azure Primary Refresh Tokens (PRT) or Illicit Consent Grants in Entra ID to bypass MFA requirements.</samp> |
| <samp><b>4. Cross-Tenant & Lateral Pivot</b></samp> | <samp>Expand the Blast Radius</samp> | <samp>Abusing Cross-Account Trusts (AWS) or peering connections. Compromising the CI/CD pipeline (GitLab/GitHub Actions runners) to inject malicious Terraform/CloudFormation code, infecting future deployments.</samp> |
| <samp><b>5. Total Control Plane Seizure</b></samp> | <samp>Absolute Persistence</samp> | <samp>Execution of <b>Golden SAML</b> attacks to forge identity provider (IdP) responses, granting immutable, unlogged access to any cloud resource. Exfiltration of S3 buckets/Azure Blobs and RDS snapshots via VPC endpoints to avoid detection.</samp> |

<br>

## <samp>▌ <u>0x03_THE_TACTICAL_ARSENAL (CLOUD)</u></samp>

<samp>To evade CloudTrail, GuardDuty, and Azure Sentinel, we do not use standard frameworks out-of-the-box. We use customized, API-native tooling:</samp>

*   **Boto3/Azure-SDK Custom Wrappers:** Proprietary Python scripts that throttle API calls and spoof User-Agents (e.g., mimicking legitimate Terraform or AWS CLI traffic) to evade heuristic detection.
*   **Shadow-SAML Forger:** Internal tool for extracting the ADFS Token-Signing Certificate from an on-premise domain and generating forged SAML assertions to bypass cloud MFA.
*   **IMDSv2-Smuggler:** Specialized SSRF payloads designed to handle the PUT requests and token headers required to bypass modern AWS metadata protections.
*   **Ephemeral Persistence Injector:** Serverless functions (AWS Lambda / Azure Functions) deployed maliciously to execute persistence tasks asynchronously without triggering EC2 alerts.

<br>

## <samp>▌ <u>0x04_ATTACK_FLOW (THE KILL-CHAIN)</u></samp>

<samp>Visual representation of the Cloud Subversion process:</samp>

```mermaid
graph TD;
    ZERO["<b>Initial Access</b><br>(SSRF / Leaked CI-CD Keys)"] --> IMDS["<b>Metadata Extraction</b><br>(IMDSv2 / Azure Instance API)"];
    IMDS --> TOKEN{"<b>Ephemeral Token Acquired</b><br>(STS / Managed Identity)"};
    
    TOKEN -- "AWS" --> AWS_ENUM["<b>IAM Policy Enumeration</b><br>(Check for iam:PassRole)"];
    TOKEN -- "Azure" --> AZ_ENUM["<b>Entra ID Enumeration</b><br>(Check for App Roles)"];

    AWS_ENUM --> LPE["<b>Vertical Escalation</b><br>(Attach Admin Policy)"];
    AZ_ENUM --> LPE;

    LPE --> PIVOT["<b>Cross-Account/Tenant Pivot</b><br>(AssumeRole / PRT Abuse)"];
    
    PIVOT --> EXFIL["<b>Data Seizure</b><br>(Clone S3/RDS Snapshots)"];
    PIVOT --> PERSIST["<b>Absolute Persistence</b><br>(Golden SAML / Backdoor IdP)"];

    style ZERO fill:#111,stroke:#666,stroke-width:1px,color:#aaa
    style IMDS fill:#111,stroke:#00adef,stroke-width:2px,color:#fff
    style TOKEN fill:#111,stroke:#f5ba14,stroke-width:2px,color:#fff
    style AWS_ENUM fill:#111,stroke:#ff8c00,stroke-width:2px,color:#fff
    style AZ_ENUM fill:#111,stroke:#4682b4,stroke-width:2px,color:#fff
    style LPE fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style PIVOT fill:#111,stroke:#ff4646,stroke-width:2px,color:#fff
    style EXFIL fill:#111,stroke:#00ff00,stroke-width:2px,color:#00ff00
    style PERSIST fill:#111,stroke:#00ff00,stroke-width:3px,color:#00ff00
```

<br>

## <samp>▌ <u>0x05_PROJECT_ARCHON_INTEGRATION (ROMERO_V34)</u></samp>

<div style="border-left: 4px solid #4682b4; padding-left: 15px; background: rgba(70, 130, 180, 0.05); padding: 15px;">
<samp>
This playbook is the core operational matrix for <b>[+] ROMERO_V34</b>.
<br><br>
When the NEXUS engages a cloud infrastructure, ROMERO ingests this doctrine to understand that physical memory corruption is useless here. Instead, it weaponizes the Cloud API. The AI learns to parse complex JSON IAM policies in milliseconds, identifying the mathematical path to privilege escalation before the Cloud Provider's telemetry engines can raise a GuardDuty alert.
</samp>
</div>

<br>

<div align="center">
<hr style="width: 80%; border: 1px solid #333;">
<br>
<samp><strong><font color="#00ADEF">WE ARE FSOCIETY. WE ARE FINALLY FREE. WE ARE FINALLY AWAKE.</font></strong></samp>
</div>
