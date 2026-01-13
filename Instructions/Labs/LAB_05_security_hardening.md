---
lab:
    title: 'Lab 05: Harden devices with security baselines'
    type: 'Answer Key'
    module: 'Learning Path 05: Secure and monitor endpoints'
---

> **Abstract:**  
> In this lab, you will deploy Windows security baselines to enforce comprehensive security settings, onboard devices to Microsoft Defender for Endpoint for advanced threat protection, configure Attack Surface Reduction (ASR) rules to block common attack vectors, and monitor security posture through the Defender portal.

# Lab 05: Harden devices with security baselines
# Student lab answer key

## Lab scenario

Continuing as **Alex Rivera**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully protected data and enforced access controls in Lab 04. Now you need to harden devices against advanced threats by deploying security baselines, integrating with Microsoft Defender for Endpoint, and configuring proactive threat prevention.

In this lab, you will deploy the Windows 11 security baseline to enforce 100+ recommended security settings, onboard enrolled devices to Defender for Endpoint for advanced threat detection and response, configure ASR rules to block credential theft and malicious scripts, and monitor device security posture and vulnerabilities through the Defender portal.

## Lab Duration

  - **Estimated Time to complete**: 45 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01-04** before starting this lab. You need at least one enrolled Windows device.

> [!NOTE]
> **License Requirements**: This lab requires **Microsoft Defender for Endpoint Plan 2** (included in Microsoft 365 E5 or standalone licenses).

## Exercise 1: Deploy Windows security baseline

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will deploy the Windows security baseline to enforce Microsoft-recommended security settings across your Windows devices.

### Task 1 - Create and deploy security baseline

1. Navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with your **Intune Administrator** credentials.

1. In the left navigation pane, expand **Endpoint security** and select **Security baselines**.

1. On the **Security baselines** page, you should see several baseline options:
    - **Security Baseline for Windows 10 and later**
    - **Microsoft Defender for Endpoint baseline** (if Defender integration is enabled)
    - **Microsoft Edge baseline**

1. Select **Security Baseline for Windows 10 and later**.

1. Select **Create profile**.

1. On the **Basics** page:
    - **Name**: `Windows 11 Security Baseline - Corporate Devices`
    - **Description**: `Microsoft-recommended security baseline with 100+ security settings for Windows 11 devices`

1. Select **Next**.

1. On the **Configuration settings** page, you will see categories of security settings:
    - **Above Lock** (lock screen settings)
    - **Application Guard** (isolated browsing)
    - **Attack Surface Reduction Rules** (blocked threats)
    - **BitLocker** (encryption settings)
    - **Browser** (Edge settings)
    - **Credential Guard** (credential protection)
    - **Data Protection** (data security)
    - **Device Guard** (code integrity)
    - **Device Installation** (hardware restrictions)
    - **Device Lock** (authentication settings)
    - **DMA Guard** (DMA attack protection)
    - **Firewall** (network protection)
    - **Local Policies Security Options** (authentication and account policies)
    - **Microsoft Defender** (antivirus and exploit protection)
    - **Microsoft Network Client** (SMB security)
    - **Microsoft Network Server** (server security)
    - **Smart Screen** (phishing protection)
    - **User Rights Assignment** (privilege restrictions)
    - **Windows Connection Manager** (network connection policies)
    - **Windows Hello for Business** (passwordless authentication)

    > [!NOTE]
    > The security baseline contains 100+ pre-configured settings based on Microsoft security team recommendations. Most settings should be left at their default (recommended) values.

1. **Optional**: Expand categories like **Microsoft Defender** and **BitLocker** to review the specific settings being enforced:
    - **Defender**: Real-time protection, cloud-delivered protection, PUA detection, scan settings
    - **BitLocker**: Device encryption, recovery key storage, startup authentication

1. Leave all settings at their **default (recommended)** values unless you have specific requirements.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Review + create** page, review the configuration and select **Create**.

You have successfully deployed the Windows security baseline to your enrolled devices.

### Task 2 - Monitor security baseline deployment

1. After creating the baseline, you are returned to the **Security baselines** page.

1. Select **Security Baseline for Windows 10 and later** to view all profiles.

1. Select the **Windows 11 Security Baseline - Corporate Devices** profile.

1. On the profile overview page, review:
    - **Device status**: Success, Pending, Error, Conflict
    - **Assignment status**: Number of assigned devices

    > [!NOTE]
    > Baseline deployment can take several hours as devices sync and apply 100+ settings. Status may show "Pending" initially.

1. Select **Device status** in the left menu to view per-device deployment results.

1. If any devices show "Error" or "Conflict," select the device to view detailed error messages.

1. Leave the browser window open for the next exercise.

## Exercise 2: Onboard devices to Microsoft Defender for Endpoint

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will configure the Microsoft Defender for Endpoint connector in Intune and onboard your enrolled devices to the Defender service.

### Task 1 - Configure Defender for Endpoint connector

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, expand **Tenant administration** and select **Connectors and tokens**.

1. On the **Connectors and tokens** page, locate **Microsoft Defender for Endpoint** and select it.

1. On the **Microsoft Defender for Endpoint** connector page, configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Connect Windows devices version 10.0.15063 and above to Microsoft Defender for Endpoint** | **On** |
    | **Connect Android devices to Microsoft Defender for Endpoint** | Optional (On if you have Android devices) |
    | **Connect iOS devices to Microsoft Defender for Endpoint** | Optional (On if you have iOS devices) |
    | **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** | **On** (allows Defender to remediate vulnerabilities via Intune) |

1. Select **Save** at the top of the page.

1. Wait for the notification: "Successfully updated Microsoft Defender for Endpoint settings."

    > [!NOTE]
    > This enables the integration between Intune and Defender for Endpoint, allowing device onboarding and security signal sharing.

1. Leave the browser window open for the next task.

### Task 2 - Create Defender for Endpoint onboarding profile

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, expand **Devices** and select **Configuration**.

1. Select the **Policies** tab.

1. Select **+ Create** → **+ New policy**.

1. On the **Create a profile** pane:
    - **Platform**: Windows 10 and later
    - **Profile type**: Templates
    - **Template name**: Select **Microsoft Defender for Endpoint (Windows 10 Desktop)**

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `Defender for Endpoint Onboarding - Windows`
    - **Description**: `Onboards Windows devices to Microsoft Defender for Endpoint for advanced threat protection`

1. Select **Next**.

1. On the **Configuration settings** page:
    - **Microsoft Defender for Endpoint client configuration package type**: **Onboard**
    - **Onboarding blob**: This field should auto-populate with the onboarding package from Defender. If blank, wait a moment and refresh.

    > [!NOTE]
    > The onboarding blob is automatically retrieved from the Defender for Endpoint tenant once the connector is enabled.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Review + create** page, review and select **Create**.

You have successfully created the Defender for Endpoint onboarding profile.

### Task 3 - Verify device onboarding in Defender portal

1. Open a new browser tab and navigate to the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. Sign in with your **Security Administrator** or **Global Administrator** credentials.

1. In the left navigation pane, expand **Assets** and select **Devices**.

1. On the **Device inventory** page, wait 5-15 minutes for your enrolled devices to appear after the onboarding policy is applied.

    > [!NOTE]
    > Device onboarding can take 15-30 minutes after policy is applied. Devices must sync with Intune and then communicate with the Defender service.

1. Once your devices appear, you should see both **SEA-WS1** and **SEA-WS2** in the inventory.

1. Select **SEA-WS1** to view details:
    - **Onboarding status**: Active ✅
    - **Risk level**: Low, Medium, High (based on detected threats)
    - **Sensor health**: Active, Inactive, Misconfigured
    - **Last seen**: Timestamp of most recent check-in
    - **Threat detections**: Number of active alerts

1. Review the device details page showing:
    - **Timeline**: Security events and activities
    - **Security recommendations**: Actions to improve device security
    - **Installed software**: Detected applications
    - **Discovered vulnerabilities**: CVEs affecting installed software

1. Go back to the device inventory and select **SEA-WS2** to view its details.

1. Compare the security posture of both devices:
    - Risk levels
    - Security recommendations
    - Installed software inventory
    - Vulnerability counts

    > [!TIP]
    > Having multiple devices allows you to compare security postures, identify vulnerable devices, and prioritize remediation efforts across your fleet.

1. Leave the browser window open for the next exercise.

## Exercise 3: Configure Attack Surface Reduction rules

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will configure ASR rules to block common attack techniques like credential theft, malicious scripts, and Office macro exploits.

### Task 1 - Create ASR rules policy

1. Return to the **Microsoft Intune admin center** tab.

1. In the left navigation pane, expand **Endpoint security** and select **Attack surface reduction**.

1. Select **+ Create Policy**.

1. On the **Create a policy** pane:
    - **Platform**: Windows 10, Windows 11, and Windows Server
    - **Profile**: Attack Surface Reduction Rules

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `ASR Rules - Block Common Threats`
    - **Description**: `Blocks credential theft, Office macros, script execution, and other common attack vectors`

1. Select **Next**.

1. On the **Configuration settings** page, configure the following ASR rules (set to **Block** mode):

    | Rule | Setting |
    |------|---------|
    | **Block credential stealing from the Windows local security authority subsystem (lsass.exe)** | **Block** |
    | **Block executable content from email client and webmail** | **Block** |
    | **Block all Office applications from creating child processes** | **Block** |
    | **Block Office applications from creating executable content** | **Block** |
    | **Block Office applications from injecting code into other processes** | **Block** |
    | **Block JavaScript or VBScript from launching downloaded executable content** | **Block** |
    | **Block execution of potentially obfuscated scripts** | **Block** |
    | **Block Win32 API calls from Office macros** | **Block** |
    | **Use advanced protection against ransomware** | **Block** |
    | **Block executable files from running unless they meet a prevalence, age, or trusted list criterion** | **Audit** (test first to avoid breaking legitimate apps) |

    > [!TIP]
    > Start with **Audit** mode for rules that might impact legitimate applications. Review audit events in Defender portal, then switch to **Block** mode once you've validated there are no false positives.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Review + create** page, review and select **Create**.

You have successfully configured ASR rules to protect against common attack techniques.

## Exercise 4: Monitor security posture

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will review the security posture of your devices in the Microsoft Defender portal.

### Task 1 - Review vulnerability management dashboard

1. You are in the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. In the left navigation pane, expand **Vulnerability management** and select **Dashboard**.

1. On the **Vulnerability management** dashboard, review the following metrics:

    **Exposure score** (0-1000):
    - Measures overall organizational exposure to vulnerabilities
    - Lower score = better security posture
    - Based on discovered vulnerabilities, attack surface, and breach likelihood

    **Configuration score** (0-100%):
    - Measures alignment with Microsoft security recommendations
    - Higher score = better configuration compliance
    - Based on security baseline adoption and security control implementation

    **Top security recommendations**:
    - List of prioritized actions to improve security (e.g., "Update Microsoft Office to the latest version," "Enable tamper protection," "Enable controlled folder access")

    **Vulnerable devices**:
    - Number of devices with known vulnerabilities

1. Leave the browser window open for the next task.

### Task 2 - Review security recommendations

1. You are still in the **Microsoft Defender portal** → **Vulnerability management**.

1. In the left menu, select **Recommendations**.

1. On the **Security recommendations** page, you will see a prioritized list of security improvements:
    - **Recommendation name**: Action to take (e.g., "Install security updates for Microsoft Edge")
    - **Exposed devices**: Number of affected devices
    - **Impact**: Security benefit of implementing the recommendation
    - **Effort**: Implementation difficulty (Low, Medium, High)

1. Select a recommendation to view details:
    - **Description**: What the recommendation addresses
    - **Remediation**: How to implement the fix
    - **Exposed devices**: List of affected devices
    - **Security insights**: Why this recommendation improves security

1. Some recommendations can be remediated directly through Intune. For example, select a recommendation like "Enable tamper protection":
    - If supported, you'll see an option: **Remediate via Intune**
    - This creates a configuration profile in Intune automatically

1. Leave the browser window open for the next task.

### Task 3 - Review alerts and incidents

1. You are still in the **Microsoft Defender portal**.

1. In the left navigation pane, expand **Incidents & alerts** and select **Alerts**.

1. On the **Alerts** page, review any security alerts detected on your devices:
    - **Severity**: Informational, Low, Medium, High, Critical
    - **Status**: New, In progress, Resolved
    - **Detection source**: Defender Antivirus, ASR rules, EDR, etc.
    - **Alert title**: Description of the threat (e.g., "Suspicious PowerShell execution detected")

1. Select an alert (if any exist) to view details:
    - **Alert story**: Timeline of events leading to the alert
    - **Affected assets**: Devices, users, files involved
    - **MITRE ATT&CK techniques**: Attacker tactics and techniques
    - **Recommended actions**: Response steps (isolate device, run scan, block file)

1. Review the alert story to understand what triggered the detection.

1. If no alerts exist yet, this is good news—your devices are secure! Alerts will appear when threats are detected.

## Lab Completion

Congratulations! You have successfully completed Lab 05: Harden devices with security baselines.

### Summary of what you accomplished

In this lab, you:
- ✅ Deployed Windows security baseline with 100+ Microsoft-recommended security settings
- ✅ Monitored security baseline deployment status across devices
- ✅ Configured Microsoft Defender for Endpoint connector in Intune
- ✅ Created Defender for Endpoint onboarding profile to onboard Windows devices
- ✅ Verified both SEA-WS1 and SEA-WS2 onboarding in the Defender portal
- ✅ Compared security posture across multiple devices
- ✅ Configured ASR rules to block credential theft, Office macros, script execution, and ransomware
- ✅ Reviewed vulnerability management dashboard (exposure score, configuration score)
- ✅ Reviewed security recommendations for improving device security
- ✅ Reviewed alerts and incidents to understand threat detections

### Next steps

In **Lab 06: Investigate incidents with Security Copilot (capstone)**, you will:
- Investigate security incidents using AI-powered Security Copilot
- Use natural language prompts to analyze threats and extract intelligence
- Troubleshoot device compliance issues with Copilot in Intune
- Generate investigation reports for technical and executive audiences

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 06 - Investigate incidents with Security Copilot (capstone)  
**Estimated Time for Next Lab**: 60 minutes
