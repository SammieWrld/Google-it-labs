# Windows Troubleshooting Guide

## Common Issues and Fixes

### 1. Cannot connect to Wi-Fi

Basic steps:
- Check if Wi-Fi is turned on
- Restart the router
- Run the Windows Network Troubleshooter (Settings > Network & Internet > Status > Network troubleshooter)

If problem persists:

- Check if airplane mode is enabled and disable it
- Verify that the wireless network adapter is enabled in Device Manager
- Update or roll back wireless network drivers in Device Manager
- Forget the Wi-Fi network and reconnect with correct password
- Check IP configuration by running `ipconfig /all` in Command Prompt to see if you have a valid IP address
- Reset TCP/IP stack using commands:
  ```bash
  netsh winsock reset
  netsh int ip reset
  ipconfig /release
  ipconfig /renew
  ipconfig /flushdns

- Try connecting to another Wi-Fi network to isolate if it’s a device or network issue
- Restart network services using:

  ```bash
  net stop dhcp
  net start dhcp
  net stop dnscache
  net start dnscache
  ```
- Check firewall settings or VPN conflicts that might block connectivity

If still unresolved:

- Escalate to Tier 2 support or network administrator for deeper diagnostics
- Check router/modem logs or settings for device restrictions
- Run hardware diagnostics on wireless adapter


### 2. Slow computer performance

Basic steps:

- Close unnecessary programs
- Check for malware using antivirus software
- Run Disk Cleanup (type “Disk Cleanup” in search)

If problem persists:

- Check Task Manager for high CPU, memory, or disk usage to identify resource-heavy processes
- Disable unnecessary startup programs using Task Manager or `msconfig`
- Ensure Windows and drivers are up to date via Windows Update and Device Manager
- Run System File Checker (SFC) to repair corrupted system files:
  ```bash
  sfc /scannow
  
- Run DISM tool to repair Windows image:
```bash
  DISM /Online /Cleanup-Image /RestoreHealth
  ```

- Check available disk space and free up space if low
- Scan for hardware issues like failing hard drive using tools such as CHKDSK:
  ```bash
  chkdsk /f /r
  ```
  
- Consider performing a clean boot to troubleshoot software conflicts
- Review recent software or driver installations that might be causing issues and uninstall if necessary

If still unresolved:

- Back up important data and consider system restore to a previous point when performance was normal
- Escalate to IT support or technician for deeper hardware diagnostics (RAM, HDD/SSD health, thermal issues)
- Consider reinstalling Windows as a last resort after data backup

### 3. Printer not printing

Basic steps:

- Check printer power and connections
- Restart printer and computer
- Reinstall printer drivers via Device Manager

If problem persists:

- Verify the printer is set as the default printer in Windows Settings
- Check printer queue for stuck print jobs and clear them
- Ensure printer firmware is up to date (check manufacturer’s website)
- Run the built-in Windows Printer Troubleshooter (Settings > Update & Security > Troubleshoot > Printer)
- Check if the printer is connected to the correct network (for network printers) or USB port
- Try connecting the printer to a different USB port or computer to isolate hardware issues
- Temporarily disable firewall or antivirus software to see if they are blocking print jobs
- Check for any error messages or blinking lights on the printer and refer to the user manual

If still unresolved:

Escalate to Tier 2 support or printer manufacturer support for advanced diagnostics
Consider replacing cables or printer hardware if diagnosed as faulty


This guide is a work in progress. More tips coming soon!
