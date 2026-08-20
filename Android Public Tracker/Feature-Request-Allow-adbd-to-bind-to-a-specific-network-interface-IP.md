Where: [**Feature Request: Allow adbd to bind to a specific network interface/IP**](https://issuetracker.google.com/issues/526109803) on [Android Issue Tracker](https://issuetracker.google.com)

Who: Google account 沈威宇 cg10250207@gmail.com

---

I support the proposed "Allowed Network Interfaces" setting under Developer Options > Wireless Debugging, as restricting "adbd" to selected interfaces would significantly reduce the attack surface of future vulnerabilities.

My main concern is that loopback ("127.0.0.1") ADB should continue to be supported, with an explicit opt-in implementation proposed.

Without loopback ADB, I see four major impacts:

1. Automation workflows. While most of my own automation in Macrodroid and AutoJs6 could eventually be recreated by granting `android.permission.WRITE_SECURE_SETTINGS` once from a computer to the apps and relying on it and Accessibility services, this is not true for every use case. Many automations, especially accessibility-oriented ones, depend on loopback ADB. In addition, not every user has access to a computer for the `android.permission.WRITE_SECURE_SETTINGS` initialization. Relying on OEMs to implement every missing capability is unfortunately not realistic.
2. Manual workflows. Workflows involving manual call to local ADB or its abstraction, notably Shizuku, will no longer function. They include ADB server or Shizuku ADB shell on Termux or other terminal apps, Hail, InstallerX Revived, SD Maid SE, LogFox, and other applications. I regularly enable and disable applications, adjust AppOps and compatibility flags (for example "SYSTEM_EXEMPT_FROM_DISMISSIBLE_NOTIFICATIONS"), inspect logcat, and perform other debugging tasks directly from my phone to
adjust preferences, test apps, and improve my privacy and phone performance.
3. Convenience and security of adjusting settings. Sometimes the settings app is inconvenient when adjusting some settings since it often loads for a long time, needs manual toggling of a long list, or is confusing for some users. Apps utilizing Shizuku can grant permissions, change default apps, etc. more easily for users. This still requires explicit user interaction and can prevent potential misconfiguration.
4. Potentially worse security for some users. Personally, I would likely delay system and some application updates and decrease reboot frequency because I may have to reconnect to a computer after updates to restore my ADB settings, system apps uninstallation and disabling, and some ADB-based workflow after an reboot or update. That is an unintended incentive.

Another issue is that Wireless Debugging currently requires a Wi-Fi connection before it can even be enabled in Developer Options. This means that after every reboot, users who rely on on-device ADB must either connect to a Wi-Fi network—potentially an untrusted public network—or have access to a computer before they can pair Shizuku again.

My proposal is therefore:

- Keep secure defaults.
- Add an explicit Developer Options option that allows loopback-only ADB and other interfaces.
- When loopback-only ADB is enabled, "adbd" should bind only to "127.0.0.1"/"::1", without exposing any external network interface, unless other interfaces are also explicitly allowed.
- This mode should not require a Wi-Fi connection or an external computer to be able to be toggled by the user.

This preserves the security benefits of restricting network exposure while continuing to support legitimate on-device developer workflows.

I would also argue that Shizuku and loopback ADB can improve security for advanced users in some scenarios. For example:

- They allow temporary workarounds for platform bugs until official fixes are released (such as modifying device_config to mitigate the recent Android 16 VPN leak).
- They enable one-time application installation through tools such as InstallerX Revived without permanently granting an app the "Install unknown apps" permission.
- They provide a non-root alternative for many advanced tasks. Removing this option may encourage some users to root their devices instead, which generally carries a much larger security impact than an explicitly enabled loopback-only ADB mode.

For these reasons, I believe configurable interface binding with an explicit loopback-only option offers the best balance between improving ADB's security posture and preserving valuable developer and power-user workflows.

