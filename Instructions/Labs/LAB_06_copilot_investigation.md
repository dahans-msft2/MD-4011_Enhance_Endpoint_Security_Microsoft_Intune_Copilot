---
lab:
    title: 'Lab 06: Investigate incidents with Security Copilot (Capstone)'
    type: 'Answer Key'
    module: 'Learning Path 06: Investigate and respond with Security Copilot'
---

> **Abstract:**  
> In this capstone lab, you will use Microsoft Security Copilot to investigate security incidents using natural language prompts, analyze suspicious scripts with AI-powered decoding, troubleshoot device compliance issues in Intune, and generate investigation reports for technical and executive audiences. This lab demonstrates how AI accelerates security operations and empowers analysts of all skill levels.

# Lab 06: Investigate incidents with Security Copilot (Capstone)
# Student lab answer key

## Lab scenario

Congratulations on reaching the capstone lab! As **Alex Rivera**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully deployed Intune, enrolled devices, configured policies, protected data, and hardened endpoints in Labs 01-05.

Now, Contoso's Security Operations Center (SOC) has detected a high-severity alert: Suspicious PowerShell activity on a Finance department device suggesting a credential theft attempt. As part of the security team, you will use Microsoft Security Copilot to investigate this incident, understand the attack, troubleshoot device vulnerabilities, and generate reports for stakeholders.

This lab represents the culmination of your endpoint management and security journey, demonstrating how AI-powered Security Copilot transforms security operations from reactive to proactive, reducing investigation time from hours to minutes.

## Lab Duration

  - **Estimated Time to complete**: 60 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: 
> - You must complete **Lab 01-05** before starting this lab
> - **Microsoft Security Copilot license** with SCUs provisioned (minimum 1 SCU)
> - **Security Administrator** or **Security Copilot Contributor** role
> - Defender and Intune plugins enabled in Security Copilot

> [!NOTE]
> If you do not have a Security Copilot license, you can still review this lab to understand the capabilities. Contact your training provider or Microsoft account team to provision Security Copilot for your tenant.

## Exercise 1: Set up Security Copilot environment

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will verify Security Copilot is available, check SCU capacity, and enable required plugins for Defender and Intune integration.

### Task 1 - Access Security Copilot portal

1. Open **Microsoft Edge** and navigate to the **Microsoft Security Copilot portal** at [**https://securitycopilot.microsoft.com**](https://securitycopilot.microsoft.com/).

1. Sign in with your **Security Administrator** or **Security Copilot Contributor** credentials.

1. If this is your first time accessing Security Copilot, you may see a welcome screen explaining the service. Review and dismiss it.

1. You should land on the **Security Copilot Home** page showing:
    - **Prompt bar** at the bottom for entering natural language queries
    - **Session history** on the left (previous investigations)
    - **Suggested prompts** to get started
    - **Plugins** button in top-right to manage integrations

1. Leave the browser window open for the next task.

### Task 2 - Verify SCU capacity and consumption

1. You are on the **Security Copilot Home** page.

1. In the top-right corner, select the **gear icon** (Settings).

1. In the Settings pane, select **Capacity**.

1. On the **Capacity** page, review:
    - **Provisioned SCUs**: Number of Security Compute Units allocated to your tenant (minimum 1 SCU required)
    - **Current usage**: Real-time SCU consumption
    - **Usage history**: Historical consumption trends

    > [!NOTE]
    > Each prompt and response consumes SCUs based on complexity. 1 SCU = approximately 1 million Security Copilot operations per month. For labs, 1-2 SCUs are sufficient.

1. If SCUs are not provisioned or capacity is 0, you will need to contact your administrator to provision Security Copilot capacity before continuing.

1. Close the Settings pane.

### Task 3 - Enable Defender and Intune plugins

1. You are on the **Security Copilot Home** page.

1. In the top-right corner, select **Plugins** (puzzle piece icon).

1. On the **Plugins** page, you will see available plugins:
    - **Microsoft Defender XDR** (includes Defender for Endpoint, Defender for Office 365, Defender for Identity)
    - **Microsoft Intune**
    - **Microsoft Entra** (identity and access)
    - **Microsoft Purview** (compliance and data governance)
    - **Natural Language to KQL** (query assistance)
    - **Public web search** (threat intelligence from the web)

1. Ensure the following plugins are **Enabled** (toggle to On):
    - ✅ **Microsoft Defender XDR**
    - ✅ **Microsoft Intune**

1. If either plugin is disabled, toggle it to **On**.

    > [!IMPORTANT]
    > These plugins allow Security Copilot to query incidents, devices, and security data from Defender and Intune. Without them, Copilot cannot investigate incidents or troubleshoot devices.

1. Close the Plugins pane.

You have successfully verified Security Copilot is ready for use with Defender and Intune integration.

## Exercise 2: Investigate security incident with Copilot

### Exercise Duration

  - **Estimated Time to complete**: 20 minutes

In this exercise, you will investigate a high-severity security incident using Security Copilot in the Defender portal. You will use natural language prompts to understand the attack, analyze malicious scripts, and get guided response recommendations.

### Task 1 - Access incident in Defender portal with Copilot

1. Open a new browser tab and navigate to the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. Sign in with your **Security Administrator** credentials.

1. In the left navigation pane, expand **Incidents & alerts** and select **Incidents**.

1. On the **Incidents** page, you should see a list of security incidents. If you don't have any incidents, you can:
    - **Option A**: Wait for real incidents to be detected (can take days/weeks)
    - **Option B**: Use the **Microsoft Defender evaluation lab** to simulate attacks and generate incidents (recommended for training)
    - **Option C**: Proceed with this task using a hypothetical scenario and review the Copilot interface

    > [!TIP]
    > To access the Defender evaluation lab: Select **Evaluation & tutorials** in the left menu → **Evaluation lab** → Set up lab. This creates a simulated environment with pre-configured attack scenarios.

1. Select a **high-severity incident** from the list (or imagine a scenario: "Suspicious PowerShell execution detected on SEA-WS1" or "SEA-WS2").

1. On the incident details page, look for the **Copilot** button in the top-right toolbar or a **Copilot** pane on the right side.

1. If the Copilot pane doesn't appear automatically, select the **Copilot** button to open it.

1. The Copilot pane should display an **automatic incident summary** generated by AI:
    - **Attack type**: Description of the attack (e.g., "Potential credential theft using PowerShell-based tools")
    - **Timeline**: Sequence of events
    - **Affected assets**: Devices, users, files involved
    - **MITRE ATT&CK techniques**: Attacker tactics and techniques (e.g., T1003 - Credential Dumping, T1059 - PowerShell execution)
    - **Recommended actions**: Immediate response steps

1. Review the automatic summary. This analysis would normally take 30+ minutes of manual log review, but Copilot provides it instantly.

1. Leave the browser window open for the next task.

### Task 2 - Use natural language prompts to investigate

1. You are viewing the incident with the **Copilot pane** open in the Defender portal.

1. In the Copilot **prompt bar** at the bottom, type the following prompt:

    **Prompt**: `What PowerShell commands were executed on the affected device?`

1. Press **Enter** and wait for Copilot to respond (5-15 seconds).

1. Copilot analyzes the incident data and provides a response showing:
    - Decoded PowerShell commands (if obfuscated)
    - Command purpose (e.g., "Attempts to dump credentials from LSASS process memory")
    - Parameters and arguments used

1. Review the response. Copilot has automatically decoded and explained the PowerShell script.

1. Ask a follow-up question. Type the following prompt:

    **Prompt**: `Is the IP address 185.220.101.45 known malicious?`

    > [!NOTE]
    > Replace the IP address with one from your actual incident, or use this example for demonstration.

1. Press **Enter**.

1. Copilot queries threat intelligence databases and responds with:
    - IP reputation (Malicious, Suspicious, Clean)
    - Associated threat actors or campaigns
    - Related indicators of compromise (IOCs)

1. Ask another question to understand the attack chain:

    **Prompt**: `What MITRE ATT&CK techniques were used in this attack?`

1. Press **Enter**.

1. Copilot responds with a list of MITRE ATT&CK techniques:
    - **T1059.001** - PowerShell execution
    - **T1003.001** - LSASS memory dumping
    - **T1021** - Lateral movement attempts

1. Review the techniques to understand the attacker's tactics.

    > [!TIP]
    > Each answer helps you build a more complete picture of the attack. Copilot enables conversational investigation—ask questions as they occur to you, just like talking to a senior analyst.

1. Leave the browser window open for the next task.

### Task 3 - Analyze suspicious script with Copilot

1. You are still viewing the incident in the **Defender portal** with **Copilot** open.

1. In the incident timeline, locate an alert related to **PowerShell script execution** or **suspicious file execution**.

1. If your incident has a script or file, select **Analyze script** (or ask Copilot directly).

1. In the Copilot prompt bar, type:

    **Prompt**: `Analyze the PowerShell script from this alert`

1. Press **Enter**.

1. Copilot performs script analysis and provides:
    - **Decoded script**: Human-readable version of obfuscated code
    - **Script purpose**: Plain English explanation (e.g., "Attempts to dump credentials from LSASS process memory and exfiltrate to external server")
    - **Malicious behaviors**: Memory access, process injection, encoding/decoding, network connections
    - **Verdict**: Malicious, Suspicious, or Benign
    - **IOCs**: File hashes, command patterns, registry keys, network indicators

1. Review the script analysis. This would normally require malware reverse engineering skills and 30+ minutes of analysis. Copilot provides it in 10 seconds.

1. Leave the browser window open for the next task.

### Task 4 - Review guided response recommendations

1. You are still viewing the incident with **Copilot** open.

1. In the Copilot pane, locate the **Guided response** section (or ask: `What should I do to remediate this incident?`).

1. Copilot provides a prioritized list of response actions:
    - ✅ **Isolate affected device** from network to prevent lateral movement
    - ✅ **Reset passwords** for users active on the device during the attack
    - ✅ **Run full antivirus scan** to detect additional malware
    - ✅ **Remove persistence mechanisms** (scheduled tasks, startup programs)
    - ✅ **Block malicious file hashes** across environment using Defender policies
    - ✅ **Monitor for lateral movement** to other devices in the network

1. Review the recommendations. Each action is tailored to the specific attack type.

1. **Optional**: If you want to take action, you can select one of the recommendations (e.g., **Isolate device**) and Copilot will guide you through the process or perform it automatically (depending on permissions).

    > [!WARNING]
    > Only isolate devices in a lab/training environment. Device isolation disconnects the device from the network, which can disrupt users.

1. Leave the browser window open for the next exercise.

## Exercise 3: Troubleshoot device with Copilot in Intune

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will use Security Copilot in the Intune admin center to troubleshoot device compliance issues and compare device configurations.

### Task 1 - Access device in Intune with Copilot

1. Open a new browser tab and navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with your **Intune Administrator** credentials.

1. In the left navigation pane, expand **Devices** and select **All devices**.

1. Select your **enrolled Windows device** from Lab 02 (or select the device involved in the incident from Exercise 2).

1. On the device details page, look for the **Copilot** button in the top-right toolbar.

1. Select **Copilot** to open the Copilot pane.

1. The Copilot pane should display an **automatic device summary**:
    - **Device name**, OS version, last sync timestamp
    - **Management state**: Compliant or Noncompliant
    - **Compliance issues**: List of failed compliance checks (e.g., "BitLocker not enabled," "Password complexity not met")
    - **Installed apps**: Microsoft 365 Apps, Teams, Edge, etc.
    - **Group memberships**: All Windows Devices, Device Management Pilot Users
    - **Applied policies**: Configuration profiles and compliance policies assigned to the device

1. Review the automatic summary. This provides instant visibility into device health and compliance.

1. Leave the browser window open for the next task.

### Task 2 - Diagnose compliance failure with Copilot

1. You are viewing your device in **Intune** with **Copilot** open.

1. In the Copilot prompt bar, type the following prompt:

    **Prompt**: `Why is this device noncompliant?`

1. Press **Enter**.

1. Copilot analyzes the device compliance data and provides an explanation:
    - **Root cause**: Specific compliance check that failed (e.g., "BitLocker encryption policy not enforced")
    - **Reason**: Why the check failed (e.g., "Group Policy conflict overrides Intune policy," "User does not have admin rights to enable BitLocker")
    - **Impact**: What this means for device security and access (e.g., "Device cannot access corporate resources via conditional access")

1. Review the explanation. Copilot identifies the root cause, not just "policy failed."

1. Ask a follow-up question:

    **Prompt**: `How do I fix the BitLocker compliance issue?`

1. Press **Enter**.

1. Copilot provides remediation steps:
    1. Check for conflicting Group Policy Objects (GPOs) in on-premises AD
    1. Ensure user has local administrator rights (required for BitLocker enablement on some devices)
    1. Manually enable BitLocker from Windows Settings → Privacy & security → Device encryption
    1. Force policy sync from Intune to re-evaluate compliance
    1. Verify compliance policy settings match device capabilities (e.g., TPM chip present)

1. Review the remediation steps. Copilot provides actionable guidance, not just "enable BitLocker."

1. Leave the browser window open for the next task.

### Task 3 - Compare SEA-WS1 and SEA-WS2 to identify configuration gaps

1. You are still viewing a device in **Intune** with **Copilot** open.

1. If you're currently viewing SEA-WS2 (which may be noncompliant or have different settings), stay on this page.

1. In the Copilot prompt bar, type:

    **Prompt**: `Compare this device to SEA-WS1`

1. Press **Enter**.

1. Copilot performs a side-by-side comparison and highlights key differences:

    **SEA-WS2 (current - personal device)**:
    - BitLocker: Not enabled (not required for personal devices)
    - Windows Security Baseline: Not applied (excluded by filter)
    - ASR rule (LSASS protection): Not configured
    - Ownership: Personal
    - Compliance: May be noncompliant

    **SEA-WS1 (corporate device)**:
    - BitLocker: Enabled
    - Windows Security Baseline: Fully applied (103 of 103 settings)
    - ASR rule (LSASS protection): Block mode
    - Ownership: Corporate
    - Compliance: Compliant

1. Copilot explains the security impact:
    - "SEA-WS2 is marked as personal ownership and excluded from corporate security policies by assignment filters"
    - "SEA-WS2 lacks critical security controls (BitLocker, ASR rules, security baseline) which increases risk of data loss and credential theft"
    - "Consider either marking SEA-WS2 as corporate-owned to apply security policies, or restricting access to sensitive resources"

1. Review the comparison. This demonstrates how assignment filters and device ownership affect policy application across your device fleet.

    > [!TIP]
    > This comparison capability is invaluable for understanding why policies apply differently across devices, troubleshooting configuration issues, and identifying security gaps in your fleet.

1. Leave the browser window open for the next exercise.

## Exercise 4: Generate investigation reports

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will use Security Copilot to generate investigation reports for different audiences: a technical report for the SOC team and an executive summary for leadership.

### Task 1 - Generate technical investigation report

1. Return to the **Microsoft Defender portal** tab (or open [**https://security.microsoft.com**](https://security.microsoft.com/) in a new tab).

1. Navigate to the **incident** you investigated in Exercise 2.

1. Open the **Copilot** pane.

1. In the Copilot prompt bar, type:

    **Prompt**: `Generate a detailed technical report for this incident`

1. Press **Enter**.

1. Copilot generates a comprehensive technical report including:

    **Incident Summary**:
    - Incident ID, severity, detection time
    - Attack type: Credential theft using PowerShell-based LSASS dumping

    **Affected Assets**:
    - Devices: FINANCE-WS01 (Windows 11)
    - Users: FinanceUser@contoso.com
    - Files: Mimikatz.exe, dump.dmp

    **Attack Details**:
    - PowerShell commands executed
    - LSASS process memory access attempts
    - Network connections to external IP (185.220.101.45)
    - Indicators of Compromise (IOCs): File hashes, registry keys, command patterns

    **Root Cause Analysis**:
    - ASR rule for LSASS protection was in Audit mode, not Block mode
    - Device lacked BitLocker encryption
    - User had local administrator rights (overprivileged)

    **Response Actions Taken**:
    - Device isolated from network
    - User password reset
    - Malicious file hashes blocked across environment
    - ASR rule changed to Block mode

    **Recommendations for Prevention**:
    - Enable ASR LSASS protection in Block mode on all devices
    - Enforce BitLocker compliance via Intune policy
    - Deploy Credential Guard on all Windows devices
    - Remove local administrator rights for standard users

1. Review the report. This contains all the technical details your SOC team needs for documentation and lessons learned.

1. **Optional**: Select **Export** or **Copy** to save the report to a file or paste into your case management system.

1. Leave the browser window open for the next task.

### Task 2 - Generate executive summary report

1. You are still viewing the incident with **Copilot** open in the Defender portal.

1. In the Copilot prompt bar, type:

    **Prompt**: `Create an executive summary of this incident for the CISO`

1. Press **Enter**.

1. Copilot generates a business-focused executive summary:

    **What Happened**:
    - "Attempted credential theft attack on a Finance department device using PowerShell-based tools"

    **Impact**:
    - "Attack was detected and blocked by Defender for Endpoint. No credentials were stolen. No data was exfiltrated. One device was temporarily isolated for 2 hours."

    **Response**:
    - "Security team isolated the device within 15 minutes of detection, reset user passwords, and blocked malicious tools across the environment."

    **Root Cause**:
    - "Device had a security control (Attack Surface Reduction rule) in Audit mode instead of Block mode, which allowed the attack to proceed further than it should have."

    **Prevention**:
    - "We are deploying additional security controls (Credential Guard, stricter ASR rules) to all devices to prevent future attempts."

    **Business Impact**:
    - "Minimal disruption. User was back online within 2 hours. No customer data was at risk. No regulatory reporting required."

1. Review the executive summary. It uses business language (not technical jargon) and focuses on impact, response, and risk to the organization.

1. **Optional**: Copy and paste the summary into an email or presentation for leadership.

## Exercise 5: Course capstone reflection

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this final exercise, you will reflect on your complete journey from Lab 01 to Lab 06 and understand how all the pieces fit together.

### Task 1 - Review the complete journey

1. Take a moment to reflect on what you've accomplished across all 6 labs:

    **Lab 01 - Configure tenant for device management**:
    - ✅ Verified licensing and assigned Intune licenses
    - ✅ Configured Entra ID for automatic MDM enrollment
    - ✅ Created dynamic device groups and security groups
    - ✅ Verified Intune tenant readiness

    **Lab 02 - Enroll and validate devices**:
    - ✅ Joined SEA-WS1 to Entra ID with automatic Intune enrollment
    - ✅ Enrolled SEA-WS2 with a different user (Allan Deyoung)
    - ✅ Validated both device enrollments in Entra ID and Intune portals
    - ✅ Reviewed device properties, compliance, and group membership
    - ✅ Performed device synchronization

    **Lab 03 - Implement policy layering and compliance**:
    - ✅ Created configuration profiles to enforce BitLocker encryption
    - ✅ Created compliance policies defining security requirements
    - ✅ Marked SEA-WS1 as corporate and SEA-WS2 as personal
    - ✅ Used filters to target corporate devices only
    - ✅ Validated policy application differences across both devices

    **Lab 04 - Protect data with MAM and conditional access**:
    - ✅ Created app protection policies for iOS and Android
    - ✅ Configured conditional access policies requiring compliant devices
    - ✅ Tested access on SEA-WS1 (compliant - granted access)
    - ✅ Tested access on SEA-WS2 (noncompliant - blocked access)
    - ✅ Compared conditional access policy evaluation across both devices

    **Lab 05 - Harden devices with security baselines**:
    - ✅ Deployed Windows security baseline with 100+ settings
    - ✅ Onboarded both SEA-WS1 and SEA-WS2 to Microsoft Defender for Endpoint
    - ✅ Compared security posture across both devices
    - ✅ Configured Attack Surface Reduction rules
    - ✅ Monitored security posture and vulnerabilities

    **Lab 06 - Investigate incidents with Security Copilot (today)**:
    - ✅ Investigated security incident with AI-powered analysis
    - ✅ Used natural language prompts to extract threat intelligence
    - ✅ Analyzed malicious scripts with automated decoding
    - ✅ Troubleshot device compliance issues with Copilot
    - ✅ Compared SEA-WS1 and SEA-WS2 configurations to identify security gaps
    - ✅ Generated technical and executive investigation reports

1. You have now mastered the **complete modern endpoint management and security lifecycle** with Microsoft Intune, Defender for Endpoint, and Security Copilot.

### Task 2 - Understand the time savings

1. Review the investigation time comparison:

    | Investigation Step | Traditional Time | With Copilot | Time Saved |
    |-------------------|------------------|--------------|------------|
    | Initial alert triage | 15-30 min | 2-3 min | 85% |
    | Threat intelligence lookup | 20-30 min | 10 sec | 98% |
    | Script analysis | 30-45 min | 10 sec | 99% |
    | Device compliance check | 15-20 min | 2 min | 90% |
    | Documentation & reporting | 30-45 min | 30 sec | 99% |
    | **Total** | **2-3 hours** | **15-20 min** | **85% overall** |

1. **Key takeaway**: Security Copilot reduces investigation time by 85%, enabling your SOC team to handle 3x more incidents with the same headcount.

1. **Empowerment**: Junior analysts can perform at senior analyst level with AI assistance. This democratizes expert-level security operations.

## Lab Completion

🎉 **Congratulations!** You have successfully completed Lab 06: Investigate incidents with Security Copilot, and with it, the entire MD-4011 course!

### Summary of what you accomplished in this lab

- ✅ Verified Security Copilot access, SCU capacity, and enabled Defender/Intune plugins
- ✅ Investigated security incident using Copilot automatic summaries and natural language prompts
- ✅ Analyzed suspicious PowerShell scripts with AI-powered decoding and threat intelligence
- ✅ Reviewed guided response recommendations for incident remediation
- ✅ Troubleshot device compliance issues using Copilot in Intune
- ✅ Compared SEA-WS1 and SEA-WS2 configurations to identify security gaps and policy differences
- ✅ Generated technical investigation report for SOC team
- ✅ Generated executive summary for leadership
- ✅ Reflected on the complete 6-lab journey from tenant setup to AI-powered security operations

### Course completion message

**You have now completed the entire MD-4011 course: Deploy, manage, and secure endpoints with Microsoft Intune.**

You started with a blank Microsoft 365 tenant and built a complete modern endpoint management and security solution:
- 📋 Configured licensing and automatic enrollment
- 💻 Enrolled Windows devices
- 🔒 Deployed configuration and compliance policies
- 🛡️ Protected data with MAM and conditional access
- 🔐 Hardened devices with security baselines and Defender
- 🤖 Investigated threats with AI-powered Security Copilot

**You now have the knowledge and skills to:**
- Deploy and manage devices at scale with Microsoft Intune
- Enforce security and compliance requirements
- Protect corporate data on managed and unmanaged devices
- Integrate with Microsoft Defender for Endpoint for advanced threat protection
- Leverage AI with Security Copilot to accelerate security operations

Contoso Healthcare went from inconsistent, insecure device management to a modern, AI-powered security operations model. **Your organization can achieve the same transformation.**

### Next steps in your journey

- **Get certified**: Microsoft Certified: Endpoint Administrator Associate (MD-102)
- **Explore advanced topics**: Windows Autopilot, app deployment, app packaging, co-management with Configuration Manager
- **Stay updated**: Microsoft Intune and Defender for Endpoint release new features monthly—stay current with [aka.ms/intunewhatsn ew](https://aka.ms/intunewhatsnew)
- **Join the community**: Microsoft Tech Community forums for Intune and Defender

### Thank you!

Thank you for completing the MD-4011 labs. We hope you found them valuable and applicable to your real-world scenarios.

---

**Lab Status**: ✅ Complete  
**Course Status**: ✅ MD-4011 Complete  
**Next Steps**: Get certified, implement in production, continue learning!
