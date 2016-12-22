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
- Outbound Rules : Block Port 53 traffic to a specific IP. Be sure to select "Custom" when making the rule.
- Outbound Rules : Block port 53 traffic to all IPs except for one. For example, say we want to allow port 53 traffic to 174.7.6.100. We can block 0.0.0.1 - 174.7.6.99 and 174.7.6.101 - 255.255.255.255. Notice we didn't list 174.7.6.100 as an IP to block. Be sure to select "Custom" when making the rule.
