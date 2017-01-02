# Group_Policy
A series of GPO templates<br>
<br>



# Blocking DNS Tunneling
### Computer Configuration -> Windows Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...-> Outbound Rules
- Outbound Rules : Block Port 53 traffic to a specific IP. Be sure to select "Custom" when making the rule.
- Outbound Rules : Block port 53 traffic to all IPs except for one. For example, say we want to allow port 53 traffic to 174.7.6.100. We can block 0.0.0.1 - 174.7.6.99 and 174.7.6.101 - 255.255.255.255. Notice we didn't list 174.7.6.100 as an IP to block. Be sure to select "Custom" when making the rule.

# Block Malicious Host
### Computer Configuration -> Windows Settings -> Security Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...-> Inbound Rules
- Inbound Rules : Drops all traffic from a specific host. The rule should have the following settings: Custom Rule, All Programs, Protocol Type: Any, Local Address: Any IP, Remote Address: <SPECIFY BAD IP HERE>, Block connection.

### Computer Configuration -> Windows Settings -> Security Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...-> Outbound Rules
- Outbound Rules : Drops all traffic to a specific host. The rule should have the following settings: Custom Rule, All Programs, Protocol Type: Any, Local Address: Any IP, Remote Address: <SPECIFY BAD IP HERE>, Block connection.

# Firewall Settings
### Computer Configuration -> Windows Settings -> Security Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security
- Enable Logging : Properties -> Logging
- Disable rules created locally to merge with GPO rules : Properties -> Settings -> Rule Merging

# Enable WMI
### Computer Configuration -> Windows Settings -> Security Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...-> Inbound Rules
- Inbound Rules : Select the predefined rule for Windows Management Instrumentation and this will create three rules.

### Computer Configuration -> Administrative Templates -> Network Connections -> Windows Firewall -> Domain Profile (Do Standard Profile as well)
- Windows Firewall: Allow inbound remote administration exception : Enabled it and add the applicable IP(s).

# Allow ICMP
### Computer Configuration -> Administrative Templates -> Network Connections -> Windows Firewall -> Domain Profile (Do Standard Profile as well)
- Windows Firewall:Allow ICMP Exceptions : Once enabled, it will allow ICMP traffic.

# Allow SMB
### Computer Configuration -> Administrative Templates -> Network Connections -> Windows Firewall -> Domain Profile (Do Standard Profile as well)
- Windows Firewall:All inbound file and printer sharing exception : Enabled it and add the applicable IP(s). Once done, this will allow SMB. traffic from the specified IPs.

# Disable Command Prompt
### User Configuration -> Policies -> Administrative Templates -> System
- Prevent access to the command prompt : Enabled it and the command prompt will be disabled

# Disable VBS
### Computer Configuration -> Preferences -> Windows Settings -> Registry
- Enabled (Value Name) : CREATE this Value in HKLM\Software\Microsoft\Windows Script Host\Settings and set it (REG_DWORD) to "0"

# Enable PowerShell Module Logging (v3 and above)
### Computer Configuration -> Policies -> Administrative Templates -> Windows Components -> Windows PowerShell
- Turn on Module Logging : Input "*". This will generate Event ID 4103 (Application & Service Logs -> Microsoft -> Windows -> PowerShell -> Operational) and works with PowerShell v3 and newer.

# Enable PowerShell Transcription (v5 and above)
### Computer Configuration -> Policies -> Administrative Templates -> Windows PowerShell
- Turn on PowerShell Transcription - Input a directory to store the data. If no directory is configured, the data will be stored in the user's Documents folder. Select the option to include invocation headers.

# Enable PowerShell Script Logging (v5 and above)
### Computer Configuration -> Policies -> Administrative Templates -> Windows PowerShell
- Turn on PowerShell Script Block Logging - Select the option to log start\stop events. Enabling this policy will generate Event IDs 4104, 4105, and 4106 (Application & Service Logs -> Microsoft -> Windows -> PowerShell -> Operational) and works with PowerShell v5 and newer.

# Enable PowerShell Execution Policy
### User Configuration -> Policies -> Administrative Template -> Windows PowerShell
- Turn on Script Execution : Enable it and select the applicable Execution Policy

# Enable "Last Modified" Value
### Computer Configuration -> Preferences -> Windows Settings -> Registry
- NtfsDisableLastAccessUpdate : CHANGE this Value in HKLM\System\CurrentControlSet\Control\FileSystem to be "0"

# Enable Remote Registry
### Computer Configuration -> Policies -> Windows Settings -> Security Settings -> System Services
- RemoteRegistry : Define the Policy and set it to Automatic

# Set Who Can Add Systems to the Domain
### Computer Configuration -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment
- Add Workstations to the Domain : Enable this and speicify a group. If this is not defined, every authenticated domain user can add 10 workstations to the domain by default.

# Enable Prefetch (Disabled by default on Servers)
### Computer Configuration -> Preferences -> Windows Settings -> Registry
- EnablePrefetcher (Value Name) : UPDATE this Value in HKLM\System\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters and set it to (REG_DWORD) to "3".

# Disable IPv6
### Computer Configuration -> Preferences -> Windows Settings -> Registry
- DisabledComponents (Value Name) : CREATE this Value in HKLM\SYSTEM\CurrentControlSet\Services\TCPIP6\Parameters and set it to (REG_DWORD)"ffffffff".

# Disable Wireless
### Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Wireless Network (IEEE 802.11) Policies
- New Wireless Network Policy for Windows Vista and later : Create a new policy. On the General tab, check the option to "Use Windows WLAN AutoCOnfig service for clients". On the Network Permissions tab, check the options for "Prevent connections to ad-hoc networks" and "Prevent connections to infrastructure networks".

# Rename local Administrator account
### Computer Configuration -> Windows Settings -> Security Settings -> Local Policies -> Security Options
Accounts: Rename Administrator Account : Input the name you want to account to be rename to.

# Disable local Administrator account
### Computer Configuration -> Preferences -> Control Panel Settings -> Scheduled Tasks
- Create a new task. The Action is "Update", Run should be "powershell.exe", and Argument should be "/c net user <acount name> /ACTIVE:no". Don't select the "Run As" option. Set the task to run at two hours from the time this policy is made. That will allow enough time for a GPO update. If you have a method to update Group Policy before that, make the kick-off time sooner than 2 hours. The Administrator account should be renamed before disabling it. 

# Set Time Zone
### Computer Configuration -> Preferences -> Control Panel Settings -> Scheduled Tasks
- Create a new task. The Action is "Create", Run should be "tzutil.exe", and Argument should be '/s "Eastern Standard Time"'. Don't select the "Run As" option. Set the task to run every hour or so (environment dependent).

