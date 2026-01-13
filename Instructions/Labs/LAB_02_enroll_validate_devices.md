---
lab:
    title: 'Lab 02: Enroll and validate devices'
    type: 'Answer Key'
    module: 'Learning Path 02: Deploy and manage devices with Microsoft Intune'
---

> **Abstract:**  
> In this lab, you will enroll a Windows 11 device into Microsoft Intune using Entra join, validate the enrollment in both the Entra ID and Intune portals, and verify device properties, compliance status, and group membership. You will also perform device synchronization from both the portal and the device itself.

# Lab 02: Enroll and validate devices
# Student lab answer key

## Lab scenario

Continuing your role as **Alex Rivera**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully configured the Microsoft 365 tenant for device management in Lab 01. Now you are ready to begin enrolling devices into Intune.

For the pilot project, you will enroll a Windows 11 device using Entra join, which provides seamless single sign-on and automatic Intune enrollment. After enrollment, you will validate the device appears in both Entra ID and Intune portals, review device properties and compliance status, and verify that the device was automatically added to the "All Windows Devices" dynamic group you created in Lab 01.

## Lab Duration

  - **Estimated Time to complete**: 30 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01: Configure tenant for device management** before starting this lab. Lab 01 configured automatic MDM enrollment, which is required for devices to enroll in Intune.

> [!WARNING]
> **Device Requirements**: You need a Windows 11 device (physical or virtual machine) that is:
> - NOT currently joined to Entra ID or managed by Intune
> - NOT joined to an on-premises Active Directory domain
> - Running Windows 11 22H2 or later
> - Connected to the internet
> - You have local administrator access

## Exercise 1: Enroll Windows device using Entra join

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will join a Windows 11 device to Entra ID, which will automatically trigger MDM enrollment in Intune (thanks to the automatic enrollment configuration you completed in Lab 01).

### Task 1 - Join Windows device to Entra ID

In this task, you will connect your Windows device to your work or school account using Entra join.

1. On your **Windows 11 device**, open **Settings** by pressing **Windows key + I** (or right-click Start and select **Settings**).

1. In the Settings app, select **Accounts** from the left navigation pane.

1. Select **Access work or school**.

1. On the **Access work or school** page, you should see "No work or school accounts connected."

1. Select the **Connect** button.

1. On the **Set up a work or school account** window, enter the **email address** of one of your pilot users (e.g., `AlexW@yourtenant.onmicrosoft.com`).

    > [!TIP]
    > Use one of the test users you assigned licenses to in Lab 01.

1. Select **Next**.

1. You will be redirected to the Microsoft sign-in page. Enter the **password** for the user account.

1. If prompted, complete **multi-factor authentication** (MFA) if it is enabled for your tenant.

1. On the **You're all set!** screen, review the message:
    - "Your device has been joined to your organization's network."
    - "Your organization might control some settings and apps on this device."

1. Select **Done**.

1. You are returned to the **Access work or school** page. You should now see a connection listed:
    - **Connected to [Your Organization]'s Azure AD**
    - User account: `AlexW@yourtenant.onmicrosoft.com`
    - Status: **Connected**

1. Below the connection, you may see an **Info** button. Select it to view connection details:
    - **Device state**: Azure AD joined
    - **Management**: Enrolled in MDM (Microsoft Intune)

    > [!NOTE]
    > If "Management" shows "Pending" or "Not enrolled," wait 1-2 minutes and refresh. Automatic MDM enrollment can take a moment to complete.

1. **Close** the Settings app.

    > [!TIP]
    > You may see a notification in the Windows taskbar: "Your organization is managing this device." This confirms Intune enrollment is active.

1. Leave the device powered on and connected to the internet.

You have successfully joined the Windows device to Entra ID and automatically enrolled it in Microsoft Intune.

## Exercise 2: Validate device enrollment in Entra ID

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will validate that the enrolled device appears in the Microsoft Entra admin center and review its properties.

### Task 1 - Locate enrolled device in Entra ID

In this task, you will find your newly enrolled device in the Entra ID device inventory.

1. On your **admin workstation** (or another device), open **Microsoft Edge** and navigate to the **Microsoft Entra admin center** at [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. Sign in with your **Global Administrator** or **Intune Administrator** credentials.

1. In the left navigation pane, expand **Identity** → **Devices** and select **All devices**.

1. On the **All devices** page, locate your newly enrolled device in the list. You can search by **device name** (e.g., DESKTOP-ABC123).

    > [!NOTE]
    > If you don't see the device immediately, wait 2-3 minutes and refresh the page. Device registration can take a few moments to appear.

1. Select the **device name** to open the device details page.

1. Leave the browser window open for the next task.

You have successfully located the enrolled device in the Entra ID device inventory.

### Task 2 - Review device properties in Entra ID

In this task, you will review the device properties to understand how Entra ID tracks the device.

1. You are viewing the device details page in the **Microsoft Entra admin center**.

1. On the **Overview** tab, review the following device properties:

    | Property | Description |
    |----------|-------------|
    | **Display name** | Device name (e.g., DESKTOP-ABC123) |
    | **Device ID** | Unique identifier assigned by Entra ID (GUID) |
    | **Object ID** | Entra ID object identifier (GUID) |
    | **Join Type** | Should show **Azure AD Joined** ✅ |
    | **Operating System** | Windows 11 (or Windows 10) |
    | **OS Version** | Full OS version (e.g., 10.0.22621.0) |
    | **Registered owner** | User who joined the device (e.g., AlexW@...) |
    | **Enabled** | Yes (device is active) |
    | **MDM** | Microsoft Intune ✅ (confirms MDM enrollment) |
    | **Compliance** | Not yet evaluated (will update after compliance policy is applied) |
    | **Last activity** | Timestamp of most recent device activity |

1. In the left menu of the device details page, select **Activity logs** to view device-related events:
    - Device registered
    - Device updated
    - User signed in

1. In the left menu, select **Properties** to view additional details:
    - Device owner
    - BitLocker keys (if BitLocker is enabled)
    - Extension attributes

1. Leave the browser window open for the next exercise.

You have successfully reviewed device properties in the Microsoft Entra admin center and confirmed the device is Entra joined and enrolled in Intune.

## Exercise 3: Enroll second Windows device (SEA-WS2)

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will enroll a second Windows 11 device (SEA-WS2) into Intune using a different user account (Allan Deyoung). This will allow you to test multi-device scenarios, user-based policy targeting, and assignment filters in later labs.

### Task 1 - Join SEA-WS2 to Entra ID with different user

In this task, you will join the second workstation to Entra ID using Allan Deyoung's account.

1. On your **second Windows 11 device (SEA-WS2)**, open **Settings** by pressing **Windows key + I**.

1. In the Settings app, select **Accounts** from the left navigation pane.

1. Select **Access work or school**.

1. On the **Access work or school** page, select the **Connect** button.

1. On the **Set up a work or school account** window, enter the email address: `AllanD@yourtenant.onmicrosoft.com`

    > [!NOTE]
    > We're enrolling this second device with a different user to demonstrate user-based policy targeting and multi-user scenarios.

1. Select **Next**.

1. Enter the **password** for Allan Deyoung's account.

1. If prompted, complete **multi-factor authentication** (MFA).

1. On the **You're all set!** screen, review the confirmation message.

1. Select **Done**.

1. Verify the connection shows:
    - **Connected to [Your Organization]'s Azure AD**
    - User account: `AllanD@yourtenant.onmicrosoft.com`
    - Status: **Connected**

1. Select the **Info** button and verify:
    - **Device state**: Azure AD joined
    - **Management**: Enrolled in MDM (Microsoft Intune)

1. **Close** the Settings app.

You have successfully enrolled SEA-WS2 with Allan Deyoung's account. You now have two enrolled devices for testing multi-device scenarios.

### Task 2 - Verify both devices in Intune admin center

In this task, you will confirm both devices appear in the Intune device inventory.

1. On your **admin workstation**, navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. In the left navigation pane, expand **Devices** and select **All devices**.

1. On the **All devices** page, verify you now see **two enrolled devices**:
    - **SEA-WS1** (enrolled by AlexW@...)
    - **SEA-WS2** (enrolled by AllanD@...)

1. Select **SEA-WS2** to view its device details.

1. On the Overview tab, verify:
    - **Primary user**: Allan Deyoung
    - **Operating System**: Windows
    - **Compliance state**: Not evaluated (no policies assigned yet)
    - **Last check-in**: Recent timestamp

1. In the left menu, select **Group membership**.

1. Verify SEA-WS2 is also a member of the **All Windows Devices** dynamic group.

1. Leave the browser window open for the next exercise.

You have successfully enrolled two devices with different users, setting up the foundation for multi-device policy testing in upcoming labs.

## Exercise 4: Validate device enrollment in Intune

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will validate that the enrolled devices appear in the Microsoft Intune admin center and review management properties, compliance status, and group memberships.

### Task 1 - Locate enrolled devices in Intune

In this task, you will find your enrolled devices in the Intune device inventory.

1. Open a new browser tab and navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with the same **Intune Administrator** credentials if prompted.

1. In the left navigation pane, expand **Devices** and select **All devices**.

1. On the **All devices** page, verify you see both enrolled devices:
    - **SEA-WS1** (enrolled by Alex Wilber)
    - **SEA-WS2** (enrolled by Allan Deyoung)

    > [!NOTE]
    > Devices in Intune are identified by device name. You can also filter by OS, ownership, compliance state, or last check-in.

1. Select **SEA-WS1** to open its device details page.

1. Leave the browser window open for the next task.

You have successfully located both enrolled devices in the Microsoft Intune admin center.

### Task 2 - Review device overview and properties

In this task, you will explore the device overview page and understand the management information Intune tracks.

1. You are viewing the device details page in the **Microsoft Intune admin center**.

1. On the **Overview** tab, review the following information:

    **Device information**:
    - **Device name**: Computer name (e.g., DESKTOP-ABC123)
    - **Managed by**: Microsoft Intune
    - **Ownership**: Corporate (or Personal, depending on enrollment method)
    - **Operating System**: Windows
    - **OS version**: Full version number
    - **Compliance state**: Compliant, Not compliant, or Not evaluated
    - **Last check-in**: Timestamp of most recent device sync

    **User information**:
    - **Primary user**: User who enrolled the device (e.g., AlexW@...)
    - **User principal name (UPN)**: Full email address

    **Management details**:
    - **Entra device ID**: Links to Entra ID device record
    - **Serial number**: Hardware serial number
    - **Total storage**: Device disk capacity
    - **Free storage**: Available disk space

1. In the left menu of the device details page, select **Properties**.

1. Review additional device properties:
    - **Management name**: Device display name in Intune
    - **Category**: (Optional) Device category for organizational grouping
    - **Ownership**: Corporate vs. Personal
    - **Enroll date**: When device was enrolled
    - **Last sync**: Most recent check-in with Intune service

1. Leave the browser window open for the next task.

You have successfully reviewed device overview and properties in the Microsoft Intune admin center.

### Task 3 - Review device compliance and configuration status

In this task, you will check the device's compliance state and configuration profile status.

1. You are still viewing the device details page in the **Microsoft Intune admin center**.

1. In the left menu, select **Device compliance**.

1. On the **Device compliance** page, review:
    - **Compliance policies**: List of compliance policies assigned to this device
    - **Status**: Compliant, Not compliant, or Not evaluated

    > [!NOTE]
    > At this point, you likely have no compliance policies assigned, so the status will show **Not evaluated**. You will create compliance policies in Lab 03.

1. In the left menu, select **Device configuration**.

1. On the **Device configuration** page, review:
    - **Configuration profiles**: List of configuration profiles assigned to this device
    - **Status**: Success, Pending, Error, or Not applicable

    > [!NOTE]
    > You likely have no configuration profiles assigned yet. You will create configuration profiles in Lab 03.

1. In the left menu, select **Managed apps**.

1. Review the list of apps detected on the device:
    - Apps installed by Intune (if any)
    - Discovered apps (apps detected on the device)

1. Leave the browser window open for the next task.

You have successfully reviewed the device's compliance and configuration status.

### Task 4 - Verify dynamic group membership

In this task, you will confirm that the device was automatically added to the "All Windows Devices" dynamic group you created in Lab 01.

1. You are still viewing the device details page in the **Microsoft Intune admin center**.

1. In the left menu, select **Group membership**.

1. On the **Group membership** page, you should see the device is a member of:
    - **All Windows Devices** (Dynamic group) ✅

    > [!NOTE]
    > Dynamic group membership evaluation can take 5-10 minutes after enrollment. If the device is not yet a member, wait a few minutes and refresh the page.

1. Select the **All Windows Devices** group name to view group details.

1. On the group details page, select **Members** in the left menu.

1. Verify your enrolled device appears in the member list.

1. Go back to the device details page in Intune.

1. Leave the browser window open for the next exercise.

You have successfully verified that the device was automatically added to the "All Windows Devices" dynamic group based on the dynamic membership rule.

## Exercise 4: Perform device synchronization

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will manually trigger device synchronization from both the Intune portal and the Windows device to force the device to check in with Intune immediately.

### Task 1 - Sync device from Intune portal

In this task, you will initiate a manual sync from the Intune admin center.

1. You are still viewing the device details page in the **Microsoft Intune admin center**.

1. At the top of the device details page, locate the toolbar with device actions.

1. Select **Sync** (or the ellipsis **...** → **Sync** if the button is collapsed).

1. A confirmation message appears: **"Sync request sent successfully."**

1. The device will receive a notification to check in with Intune immediately (instead of waiting for the scheduled 8-hour sync interval).

1. Note the **Last check-in** timestamp on the device overview page. After 1-2 minutes, refresh the page and the timestamp should update to show the recent sync.

    > [!NOTE]
    > Manual sync is useful for testing policy deployment or forcing immediate compliance evaluation.

1. Leave the browser window open for the next task.

You have successfully triggered a manual sync from the Intune admin center.

### Task 2 - Sync device from Windows Settings (optional)

In this task, you will initiate a sync from the Windows device itself.

1. On your **enrolled Windows 11 device**, open **Settings** (Windows key + I).

1. Select **Accounts** → **Access work or school**.

1. Select your work or school account connection (e.g., **Connected to [Your Organization]'s Azure AD**).

1. Select the **Info** button.

1. On the **Managed by [Your Organization]** page, scroll down to the **Device sync status** section.

1. Review the sync information:
    - **Last sync**: Timestamp of most recent sync
    - **Sync status**: Success or In progress

1. Select the **Sync** button.

1. A sync operation begins. You should see:
    - "Sync is in progress"
    - After 10-30 seconds: "Sync completed successfully"

1. The **Last sync** timestamp updates to show the current time.

1. Close the Settings app.

    > [!TIP]
    > Users can manually sync their devices to receive policy updates immediately. This is helpful when troubleshooting policy deployment issues.

You have successfully initiated a manual sync from the Windows device.

## Lab Completion

Congratulations! You have successfully completed Lab 02: Enroll and validate devices.

### Summary of what you accomplished

In this lab, you:
- ✅ Joined a Windows 11 device (SEA-WS1) to Entra ID using "Access work or school"
- ✅ Automatically enrolled SEA-WS1 in Microsoft Intune via automatic MDM enrollment
- ✅ Enrolled a second device (SEA-WS2) with a different user account (Allan Deyoung)
- ✅ Located and viewed both devices in Microsoft Entra admin center
- ✅ Reviewed device properties in Entra ID (join type, OS, owner, MDM status)
- ✅ Located and viewed both devices in Microsoft Intune admin center
- ✅ Reviewed device overview, properties, compliance status, and configuration profiles
- ✅ Verified both devices were automatically added to the "All Windows Devices" dynamic group
- ✅ Performed manual device synchronization from both the Intune portal and the device

### Next steps

In **Lab 03: Implement policy layering and compliance**, you will:
- Create configuration profiles to configure device settings (BitLocker, firewall, etc.)
- Create compliance policies to define security requirements
- Use filters to target policies to specific devices
- Validate policy application and compliance evaluation

### Troubleshooting Common Issues

**Issue**: Device does not appear in Entra ID or Intune after enrollment  
**Solution**: Wait 5-10 minutes and refresh. Check that automatic MDM enrollment is enabled in Entra ID → Devices → Enrollment → Microsoft Intune (MDM user scope = All).

**Issue**: Device shows "Registered" instead of "Azure AD Joined"  
**Solution**: This indicates the device was registered (BYOD) instead of joined. To Entra join, go to Settings → Accounts → Access work or school → Connect, and ensure you select the join option (not register).

**Issue**: MDM status shows "Not enrolled" in Entra ID  
**Solution**: Check that the user has an Intune license assigned. Verify automatic MDM enrollment is configured. Try re-enrolling the device.

**Issue**: Device not in "All Windows Devices" dynamic group  
**Solution**: Dynamic group membership can take 5-15 minutes to evaluate. Force evaluation by going to the group → Properties → Reprocess members. Verify the dynamic query is correct: `(device.deviceOSType -eq "Windows")`

**Issue**: Last check-in timestamp is old (> 8 hours)  
**Solution**: Device may be offline or blocked by firewall. Manually sync from device: Settings → Accounts → Access work or school → Info → Sync. Verify device has internet connectivity.

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 03 - Implement policy layering and compliance  
**Estimated Time for Next Lab**: 45 minutes
