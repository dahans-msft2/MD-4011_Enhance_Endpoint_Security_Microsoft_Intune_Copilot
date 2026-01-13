---
lab:
    title: 'Lab 01: Configure tenant for device management'
    type: 'Answer Key'
    module: 'Learning Path 01: Plan and configure Microsoft Intune'
---

> **Abstract:**  
> In this lab, you will configure the foundational Microsoft Intune environment for Contoso Healthcare, including licensing, user accounts, permissions, and Entra ID settings to support device management. The scenario guides you through preparing the tenant for device enrollment by setting up automatic MDM enrollment, creating dynamic device groups, and verifying Intune tenant status.

# Lab 01: Configure tenant for device management
# Student lab answer key

## Lab scenario

In the labs for this course, you are taking on the role of **Alex Rivera**, Contoso Healthcare's Modern Endpoint Administrator. Contoso Healthcare is a mid-sized healthcare organization that has deployed Microsoft 365 E5 and is now ready to implement modern endpoint management with Microsoft Intune.

You have been tasked with completing a pilot project that tests device management, security, and compliance features in Microsoft Intune as they relate to Contoso's healthcare industry requirements. The organization needs to ensure all endpoints are secure, compliant, and meet regulatory requirements while maintaining user productivity.

You have just started the pilot project. In this first lab, you will prepare the Microsoft 365 tenant for device management by verifying licenses, configuring Entra ID for automatic device enrollment, creating organizational groups, and validating Intune tenant readiness. These foundational configurations will enable device enrollment and policy management in subsequent labs.

## Lab Duration

  - **Estimated Time to complete**: 30 minutes

## Instructions

### WWL Tenants - Terms of Use

> [!IMPORTANT]
> If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.
> 
> Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and is not eligible for extension.
> 
> Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

## Exercise 1: Verify licensing and assign Intune licenses

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will verify that the Microsoft 365 tenant has the appropriate licenses for Intune device management and assign Intune licenses to pilot users who will participate in testing.

### Task 1 - Sign in as Global Administrator and review available licenses

In this task, you will sign into the Microsoft 365 admin center as a Global Administrator to review the available licenses in your tenant.

1. Open **Microsoft Edge** and browse to the **Microsoft 365 admin center** at [**https://admin.microsoft.com**](https://admin.microsoft.com/).

1. On the **Sign in** screen, enter the credentials of your **Global Administrator** account (or the MOD Administrator account provided in your lab environment).

1. If prompted, complete multi-factor authentication (MFA).

1. On the **Stay signed in?** prompt, select **No**.

1. In the left navigation pane, expand **Billing** and select **Licenses**.

1. Review the available licenses in your tenant. You should see one or more of the following:
    - **Microsoft 365 E5** (includes Intune, EMS E5, Defender for Endpoint)
    - **Microsoft 365 E3** (requires separate EMS E5 license for full Intune capabilities)
    - **Enterprise Mobility + Security E5**
    - **Microsoft Intune**

1. Note the **Total licenses** and **Available licenses** for each subscription.

    > [!NOTE]
    > If you see zero available licenses, you may need to increase the quantity in your trial or paid subscription.

1. Leave the browser window open for the next task.

You have successfully reviewed the licensing status of your Microsoft 365 tenant and confirmed Intune licensing is available.

### Task 2 - Assign licenses to pilot users

In this task, you will assign Intune/EMS licenses to test users who will participate in the device management pilot.

1. You are still signed in to the **Microsoft 365 admin center** as **Global Administrator**.

1. In the left navigation pane, expand **Users** and select **Active users**.

1. Review the list of users. You should see several test users (or you may need to create them).

    > [!TIP]
    > If test users do not exist, you can create them now: Select **Add a user** at the top, enter First name, Last name, Display name, and Username, assign a password, and complete the wizard.

1. Select the checkbox next to **3-5 test users** who will participate in the pilot (for example, Alex Wilber, Allan Deyoung, Diego Siciliani, Joni Sherman).

    > [!NOTE]
    > Include your own admin user account if you plan to enroll your own device.

1. At the top of the user list, select **Manage product licenses** (or the ellipsis **...** and then **Manage product licenses**).

1. In the **Manage product licenses** pane, select **Assign more**.

1. Select the checkbox next to the following licenses:
    - **Microsoft 365 E5** (or **Microsoft 365 E3** + **Enterprise Mobility + Security E5**)

1. Expand the license details and verify the following services are enabled:
    - **Microsoft Intune**
    - **Azure Active Directory Premium P1/P2** (now called Microsoft Entra ID Premium)

1. Select **Save changes** at the bottom of the pane.

1. Once licenses are assigned, select **Done** to close the pane.

    > [!NOTE]
    > License propagation can take a few minutes. Services will be available shortly.

1. Leave the browser window open for the next exercise.

You have successfully assigned Intune/EMS licenses to pilot users, enabling them to enroll devices and access Intune services.

## Exercise 2: Configure Entra ID for device management

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will configure Microsoft Entra ID (formerly Azure Active Directory) settings to enable device join, device registration, and automatic Mobile Device Management (MDM) enrollment.

### Task 1 - Configure device join and registration settings

In this task, you will configure Entra ID to allow users to join and register their devices.

1. Open a new browser tab and navigate to the **Microsoft Entra admin center** at [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. If prompted to sign in, use the same **Global Administrator** credentials.

1. In the left navigation pane, expand **Identity** → **Devices** and select **Overview**.

1. Review the current device statistics (you may see 0 devices at this point).

1. In the **Devices** menu, select **Device settings**.

1. On the **Device settings** page, configure the following:

    | Setting | Value |
    |---------|-------|
    | **Users may join devices to Azure AD** | **All** |
    | **Users may register their devices with Azure AD** | **All** |
    | **Require Multi-Factor Authentication to register or join devices with Azure AD** | **No** (for lab purposes; enable in production) |
    | **Maximum number of devices per user** | **50** (default; adjust based on your requirements) |
    | **Local administrator setting** | **None** (default; can enable for specific scenarios) |

    > [!TIP]
    > In a production environment, you would typically restrict device join/registration to specific groups and require MFA for enhanced security.

1. At the top of the page, select **Save**.

1. Wait for the notification: "Successfully updated device settings."

1. Leave this browser tab open for the next task.

You have successfully configured Entra ID device settings to allow users to join and register devices.

### Task 2 - Configure automatic MDM enrollment

In this task, you will enable automatic MDM enrollment in Microsoft Intune so that devices automatically enroll when users join them to Entra ID.

1. You are still in the **Microsoft Entra admin center** under **Identity** → **Devices**.

1. In the **Devices** menu, select **Enrollment**.

1. On the **Enrollment** page, you will see several enrollment options:
    - **Windows Hello for Business** (optional, can configure later)
    - **Mobility (MDM and MAM)** ← This is what we need

1. Select **Microsoft Intune** (you may see it listed under **MDM** applications).

    > [!NOTE]
    > If you don't see Microsoft Intune listed, it may not be configured yet. Look for an option to **Add MDM application** and add Microsoft Intune.

1. On the **Microsoft Intune** configuration page, configure the following:

    | Setting | Value |
    |---------|-------|
    | **MDM user scope** | **All** |
    | **MAM user scope** | **None** (we'll configure MAM in a later lab) |

1. Expand **MDM Terms of Use URL**, **MDM Discovery URL**, and **MDM Compliance URL** to review the default URLs:
    - **MDM Terms of Use URL**: `https://portal.manage.microsoft.com/TermsofUse.aspx`
    - **MDM Discovery URL**: `https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc`
    - **MDM Compliance URL**: `https://portal.manage.microsoft.com/?portalAction=Compliance`

    > [!NOTE]
    > These URLs are pre-populated by Microsoft and should not be changed unless you are using a third-party MDM provider.

1. Select **Save** at the top of the page.

1. Wait for the notification: "Successfully updated Microsoft Intune configuration."

    > [!IMPORTANT]
    > With automatic MDM enrollment enabled, any device that joins Entra ID (either Entra joined or Entra registered) will automatically enroll in Intune without additional user action.

1. Leave this browser tab open for the next exercise.

You have successfully configured automatic MDM enrollment for Microsoft Intune. Devices that join Entra ID will now automatically enroll in Intune.

## Exercise 3: Create organizational groups

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will create dynamic device groups and security groups that will be used to assign policies and applications to devices in later labs.

### Task 1 - Create a dynamic device group for all Windows devices

In this task, you will create a dynamic device group that automatically includes all Windows devices enrolled in Intune.

1. You are still in the **Microsoft Entra admin center**.

1. In the left navigation pane, expand **Identity** → **Groups** and select **All groups**.

1. At the top of the **All groups** page, select **New group**.

1. On the **New Group** page, configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Group type** | **Security** |
    | **Group name** | **All Windows Devices** |
    | **Group description** | **Dynamic group containing all Windows devices managed by Intune** |
    | **Membership type** | **Dynamic Device** |

1. Under **Dynamic device members**, select **Add dynamic query**.

1. On the **Dynamic membership rules** page, configure the rule:

    | Field | Value |
    |-------|-------|
    | **Property** | **deviceOSType** |
    | **Operator** | **Equals** |
    | **Value** | **Windows** |

1. The rule syntax should appear as: `(device.deviceOSType -eq "Windows")`

1. Select **Save** at the top of the page to save the dynamic query.

1. You are returned to the **New Group** page. Select **Create** at the bottom.

1. Wait for the notification: "Group created successfully."

    > [!NOTE]
    > The dynamic group will automatically evaluate and populate with devices as they enroll. This may take a few minutes after devices are enrolled in Lab 02.

1. Leave the browser window open for the next task.

You have successfully created a dynamic device group that will automatically include all Windows devices.

### Task 2 - Create a static group for pilot users

In this task, you will create a static security group for pilot users who will participate in the device management pilot.

1. You are still in the **Microsoft Entra admin center** under **Identity** → **Groups** → **All groups**.

1. At the top of the page, select **New group**.

1. On the **New Group** page, configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Group type** | **Security** |
    | **Group name** | **Device Management Pilot Users** |
    | **Group description** | **Static group of users participating in the Intune device management pilot** |
    | **Membership type** | **Assigned** |

1. Under **Members**, select **No members selected**.

1. On the **Add members** page, search for and select the **3-5 test users** you assigned licenses to earlier (e.g., Alex Wilber, Allan Deyoung, Diego Siciliani, Joni Sherman).

1. Select **Select** at the bottom of the page.

1. Back on the **New Group** page, select **Create**.

1. Wait for the notification: "Group created successfully."

1. Leave the browser window open for the next exercise.

You have successfully created a static group for pilot users. This group can be used to assign policies and applications to specific users in later labs.

## Exercise 4: Verify Intune tenant status

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will access the Microsoft Intune admin center and verify that the Intune tenant is properly configured and ready for device enrollment.

### Task 1 - Access Intune admin center and review tenant status

In this task, you will sign into the Intune admin center and verify the tenant configuration.

1. Open a new browser tab and navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. If prompted to sign in, use the same **Global Administrator** credentials.

1. If this is your first time accessing the Intune admin center, you may see a welcome screen. Review and dismiss it.

1. In the left navigation pane, expand **Tenant administration** and select **Tenant status**.

1. On the **Tenant status** page, review the following information:

    **Tenant details**:
    - **Tenant name**: Your organization's name
    - **Tenant location**: Geographic location (e.g., North America, Europe)
    - **MDM authority**: Should show **Microsoft Intune** ✅
    - **Tenant type**: Trial or Production

    > [!IMPORTANT]
    > The **MDM authority** must be set to **Microsoft Intune** for device management. If it shows "Not set" or "Configuration Manager", Intune is not properly configured.

    **Service health and status**:
    - Review any active incidents or service degradations
    - All services should show as "Healthy" (green checkmark)

1. In the left navigation pane, expand **Tenant administration** and select **Connectors and tokens**.

1. Review the available connectors:
    - **Certificate connector** (used for SCEP/PKCS certificates)
    - **Exchange connector** (optional, for Exchange on-premises)
    - **Windows Autopilot deployment program** (we'll configure this in later modules if needed)

    > [!NOTE]
    > You don't need to configure any connectors at this time. We're just verifying they are available.

1. Leave the browser window open.

You have successfully accessed the Microsoft Intune admin center and verified that the tenant is configured with Microsoft Intune as the MDM authority.

### Task 2 - Review Intune subscription and service health

In this task, you will verify the Intune subscription is active and review service health.

1. You are still in the **Microsoft Intune admin center**.

1. In the left navigation pane, select **Home** (or select **Dashboard** if available).

1. Review the dashboard showing:
    - **Device enrollment status**: Should show 0 devices (we'll enroll devices in Lab 02)
    - **Device compliance status**: No data yet
    - **Configuration profile status**: No data yet
    - **App installation status**: No data yet

    > [!NOTE]
    > The dashboard will populate with data as you enroll devices and assign policies in later labs.

1. In the left navigation pane, expand **Tenant administration** and select **Service health and message center**.

1. Review any active advisories, incidents, or planned maintenance.

1. Select **View in Microsoft 365 admin center** to see the full service health dashboard (optional).

1. Return to the **Microsoft Intune admin center** tab.

You have successfully verified that the Intune subscription is active and services are healthy.

## Exercise 5: Verify Entra ID and Intune configuration

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this final exercise, you will verify all configurations completed in this lab are in place and ready for device enrollment.

### Task 1 - Verify automatic enrollment configuration

In this task, you will confirm that automatic MDM enrollment is properly configured.

1. Return to the **Microsoft Entra admin center** tab (or open [**https://entra.microsoft.com**](https://entra.microsoft.com/) in a new tab).

1. In the left navigation pane, expand **Identity** → **Devices** and select **Enrollment**.

1. Select **Microsoft Intune** under **Mobility (MDM and MAM)**.

1. Verify the following settings:
    - ✅ **MDM user scope**: **All**
    - ✅ **MDM Terms of Use URL**: Populated with default Microsoft URL
    - ✅ **MDM Discovery URL**: Populated with default Microsoft URL
    - ✅ **MDM Compliance URL**: Populated with default Microsoft URL

1. If any settings are incorrect, update them and select **Save**.

1. Leave this browser tab open.

You have successfully verified that automatic MDM enrollment is configured correctly.

### Task 2 - Verify groups and license assignments

In this task, you will confirm that groups and user licenses are properly configured.

1. In the **Microsoft Entra admin center**, navigate to **Identity** → **Groups** → **All groups**.

1. Verify the following groups exist:
    - ✅ **All Windows Devices** (Dynamic Device group)
    - ✅ **Device Management Pilot Users** (Assigned Security group)

1. Select **All Windows Devices** to view group details.

1. Select **Members** in the left menu.

1. Note that the group currently has **0 members** (devices will be added automatically as they enroll in Lab 02).

1. Go back to **All groups** and select **Device Management Pilot Users**.

1. Select **Members** in the left menu.

1. Verify that your **3-5 pilot users** are listed as members.

1. Navigate to the **Microsoft 365 admin center** (or switch to the existing tab).

1. Go to **Users** → **Active users**.

1. Select one of the pilot users (e.g., **Alex Wilber**).

1. In the user details pane, select **Licenses and apps**.

1. Verify the user has the following licenses assigned:
    - ✅ **Microsoft 365 E5** (or E3 + EMS E5)
    - ✅ **Microsoft Intune** service enabled

1. Close the user details pane.

You have successfully verified that groups and license assignments are correctly configured.

## Lab Completion

Congratulations! You have successfully completed Lab 01: Configure tenant for device management.

### Summary of what you accomplished

In this lab, you:
- ✅ Reviewed available licenses in the Microsoft 365 tenant
- ✅ Assigned Intune/EMS licenses to pilot users
- ✅ Configured Entra ID device settings to allow device join and registration
- ✅ Enabled automatic MDM enrollment in Microsoft Intune
- ✅ Created a dynamic device group for all Windows devices
- ✅ Created a static security group for pilot users
- ✅ Verified Intune tenant status and MDM authority
- ✅ Confirmed all configurations are in place for device enrollment

### Next steps

In **Lab 02: Enroll and validate devices**, you will:
- Enroll a Windows device using Entra join
- Validate device enrollment in Entra ID and Intune portals
- Review device properties, compliance, and applied policies
- Perform device synchronization

### Cleanup (Optional)

If you need to reset your lab environment:

1. In **Microsoft Entra admin center** → **Groups**, delete the created groups:
   - All Windows Devices
   - Device Management Pilot Users

1. In **Microsoft 365 admin center** → **Users** → **Active users**, remove license assignments from pilot users.

1. In **Microsoft Entra admin center** → **Devices** → **Enrollment**, change **MDM user scope** to **None** to disable automatic enrollment.

> [!WARNING]
> Only perform cleanup if you are not proceeding to Lab 02 immediately, as these configurations are required for the next lab.

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 02 - Enroll and validate devices  
**Estimated Time for Next Lab**: 30 minutes
