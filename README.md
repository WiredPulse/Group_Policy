# Group_Policy
A series of GPO templates<br>
<br>

# Firewall
Computer Configuration -> Windows Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...
<br>
<br>
- Enable Logging : Properties -> Logging
- Disable rules created locally to merge with GPO rules : Properties -> Settings -> Rule Merging

Computer Configuration -> Windows Settings -> Windows Firewall with Advanced Security -> Windows Firewall with Advanced Security...-> Outbound Rules
- Outbound Rules : Block Port 53 traffic to a specific IP. Be sure to select "Custom".
- Outbound Rules : Block port 53 traffic to all IPs except for one. Be sure to select "Custom".
