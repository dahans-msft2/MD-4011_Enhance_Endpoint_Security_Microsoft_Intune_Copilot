# MD-4011 Instructor Demos

This directory contains comprehensive instructor demonstration scripts for the MD-4011 course: **Modern Endpoint Management and Security with Microsoft Intune and Security Copilot**.

## Purpose

These demos are designed to:
- Provide instructors with step-by-step guidance for live demonstrations
- Reinforce key concepts from each module
- Show real-world workflows and best practices
- Bridge the gap between theory and hands-on exercises
- Demonstrate advanced scenarios that may be too complex for learner exercises

## Demo Overview

The course includes **6 instructor-led demonstrations**, one corresponding to each module:

| Demo | Module | Duration | Focus |
|------|--------|----------|-------|
| Demo A | Module 1 | 10-12 min | Tenant readiness, license assignment, and Entra ID configuration |
| Demo B | Module 2 | 10-12 min | Device enrollment (Windows Autopilot, manual enrollment) and portal validation |
| Demo C | Module 3 | 12-15 min | Policy layering, dynamic groups, compliance policies, and filters |
| Demo D | Module 4 | 10-12 min | App protection policies (MAM) and conditional access enforcement |
| Demo E | Module 5 | 12-15 min | Security baseline deployment and Microsoft Defender for Endpoint onboarding |
| Demo F | Module 6 | 15-18 min | Security Copilot incident investigation and response (capstone demo) |

**Total demo time**: ~70-84 minutes across 6 modules

## When to Use Demos

**Recommended timing**:
- Present demos **after** the corresponding module's concept units
- Present demos **before** or **instead of** learner hands-on exercises (depending on time and lab availability)
- Use Demo F (Security Copilot) as the course capstone demonstration

**Alternative approaches**:
1. **Instructor-led only**: Show all demos, learners observe and take notes
2. **Hybrid**: Show demos first, then learners attempt similar tasks in exercises
3. **Self-paced**: Learners follow demo scripts as guided labs

## Prerequisites for Instructors

To deliver these demos, instructors need:

### Environment
- **Microsoft 365 tenant** with admin access (production or demo tenant)
- **Licenses**: Microsoft 365 E5 or E3 + EMS E5 (includes Intune, Defender for Endpoint, Security Copilot)
- **Test devices**: 
  - 1-2 Windows 11 devices (for enrollment and policy demos)
  - 1 iOS or Android device (optional, for mobile enrollment demos)
  - Devices should NOT be pre-enrolled (for clean demonstration)

### Permissions
- **Global Administrator** or **Intune Administrator** role
- **Security Administrator** role (for Defender and Copilot demos)
- **Application Administrator** role (for app-based demos)

### Software
- Microsoft Edge or Chrome browser
- Remote desktop or screen sharing tool (for virtual delivery)
- PowerShell 7.x (for scripted commands)
- Company Portal app (pre-installed on demo devices)

### Preparation
- Review demo scripts **before** class
- Test all steps in your tenant **at least 24 hours before** delivery
- Bookmark key portals:
  - Microsoft Entra admin center: https://entra.microsoft.com
  - Microsoft Intune admin center: https://intune.microsoft.com
  - Microsoft Defender portal: https://security.microsoft.com
  - Microsoft 365 admin center: https://admin.microsoft.com
- Have backup screenshots/videos in case live demos encounter issues

## Demo Files

Each demo is provided as a separate markdown file with:
- **Learning objectives**: What learners should understand after the demo
- **Prerequisites**: Required setup before starting
- **Estimated duration**: Time needed for the demonstration
- **Step-by-step instructions**: Detailed walkthrough with screenshots placeholders
- **Talking points**: Key concepts to emphasize during the demo
- **Common issues**: Troubleshooting tips if things go wrong
- **Cleanup steps**: How to reset the environment after the demo

### Demo File List

1. **DEMO-A-tenant-readiness-licensing.md** - Module 1: Tenant preparation and licensing
2. **DEMO-B-device-enrollment-validation.md** - Module 2: Device enrollment workflows
3. **DEMO-C-policy-layering-compliance.md** - Module 3: Configuration and compliance policies
4. **DEMO-D-app-protection-conditional-access.md** - Module 4: Data protection and access control
5. **DEMO-E-security-baseline-defender-onboarding.md** - Module 5: Endpoint hardening
6. **DEMO-F-copilot-incident-investigation.md** - Module 6: AI-powered security operations (capstone)

## Delivery Tips

### Before Class
- ✅ Test demos in your environment 24 hours ahead
- ✅ Clear browser cache and sign out of all Microsoft portals
- ✅ Prepare a "clean" test device (factory reset or use Windows Sandbox)
- ✅ Verify licenses are assigned to test users
- ✅ Have backup plan if live demo fails (screenshots, pre-recorded video)

### During Demo
- 🎯 **Narrate what you're doing**: Explain each click and why you're doing it
- 🎯 **Show the outcome**: Don't just configure - show the result (device compliance, policy applied, alert generated)
- 🎯 **Pause for questions**: Stop after each major section to check for understanding
- 🎯 **Relate to real world**: Share experiences from production deployments
- 🎯 **Highlight common mistakes**: Show what NOT to do and why

### After Demo
- ✅ Summarize key takeaways (3-5 bullet points)
- ✅ Connect to upcoming learner exercise or next module
- ✅ Share demo environment details so learners can reference
- ✅ Clean up demo artifacts (delete test policies, unenroll devices) if needed

## Common Issues and Solutions

### Issue: "I don't see the option to create a policy"
**Solution**: Verify you have Intune Administrator or Global Administrator role. Check that Intune subscription is active in M365 admin center.

### Issue: "Device won't enroll in Intune"
**Solution**: 
- Check MDM authority is set to Intune (not Configuration Manager)
- Verify device meets OS version requirements (Windows 10 1903+ or Windows 11)
- Ensure automatic enrollment is configured in Entra ID
- Check device isn't already enrolled under a different user

### Issue: "Policy doesn't apply to test device"
**Solution**:
- Wait 8-15 minutes for policy sync (or manually sync from Company Portal)
- Verify device is in the correct group/scope for policy assignment
- Check for conflicting policies with higher priority
- Review policy assignment status in Intune portal

### Issue: "Security Copilot is not available"
**Solution**:
- Verify Security Copilot license/SCUs are provisioned
- Check that user has Security Reader or Security Administrator role
- Ensure Copilot plugins (Defender, Intune) are enabled
- Try accessing standalone Copilot portal: https://securitycopilot.microsoft.com

### Issue: "Can't see Defender data in portal"
**Solution**:
- Confirm device is onboarded to Defender for Endpoint (check onboarding status)
- Wait 15-30 minutes after onboarding for telemetry to appear
- Verify Defender for Endpoint P2 license is assigned
- Check that Defender services are running on the device

## Customization Guidance

Feel free to adapt these demos to your specific teaching style and environment:

**Customization options**:
- **Add your organization's branding**: Replace "Contoso" with your organization name
- **Use real scenarios**: Replace fictional incidents with anonymized real-world cases
- **Extend or shorten**: Add detail for advanced audiences or simplify for beginners
- **Combine demos**: Merge related demos if time is limited
- **Create variations**: Show alternative approaches (e.g., PowerShell vs. portal)

**What NOT to change**:
- Core learning objectives (these align with module content)
- Sequence of major steps (designed for logical progression)
- Safety warnings (e.g., "don't do this in production")

## Additional Resources

- **Microsoft Learn**: [Microsoft Intune documentation](https://learn.microsoft.com/mem/intune/)
- **Microsoft Learn**: [Microsoft Defender for Endpoint documentation](https://learn.microsoft.com/defender-endpoint/)
- **Microsoft Learn**: [Security Copilot documentation](https://learn.microsoft.com/security-copilot/)
- **Tech Community**: [Endpoint Manager forum](https://techcommunity.microsoft.com/t5/microsoft-intune/bd-p/Microsoft-Intune)
- **Demo environments**: [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) (free E5 sandbox)

## Feedback and Contributions

If you're an instructor delivering this course, we'd love your feedback:
- What worked well in your demos?
- What challenges did you encounter?
- What additional demos would be helpful?
- What customizations did you make?

Please share your experiences to help improve these demos for future instructors.

---

**Demo Status**: ✅ All 6 demos drafted and ready for instructor use

**Last Updated**: November 11, 2025

**Course**: MD-4011 - Modern Endpoint Management and Security with Microsoft Intune and Security Copilot
