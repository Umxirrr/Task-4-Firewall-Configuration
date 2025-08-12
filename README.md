# Task 4 – Firewall Configuration and Testing

## Objective
Configure and test a firewall on Kali Linux using UFW by allowing and denying specific ports, verifying configurations, and testing connections between machines.

## Steps Performed

# 1. Update and Install UFW
sudo apt update
sudo apt install ufw -y

# Check UFW status (initially inactive)
sudo ufw status verbose

# 2. Allow SSH Port (22/tcp)
sudo ufw allow 22/tcp
# Alternative friendly alias
sudo ufw allow OpenSSH

# 3. Enable the Firewall
sudo ufw enable
sudo ufw status numbered

# 4. Block TCP Port 23 (Telnet)
sudo ufw deny 23/tcp
# Or explicitly insert at position 1
sudo ufw insert 1 deny proto tcp from any to any port 23
sudo ufw status numbered

# 5. Install Ncat / Netcat for Testing
sudo apt install netcat-openbsd -y
sudo apt install ncat -y

# 6. Start a Listener on Port 23
sudo ncat -l 192.168.101.130 23

# If address already in use:
sudo lsof -i :23
sudo kill -9 <PID>

# 7. Find Your IP Address
ip a
# Example Output:
# inet 192.168.101.130/24 brd 192.168.101.255 scope global dynamic eth0

# 8. Test from Another Machine (Windows PowerShell)
# First enable the Telnet client in Windows:
# Press Win + R → type 'optionalfeatures' → enable Telnet Client → OK
telnet 192.168.101.130 23
# Expected Result: Connection blocked due to UFW deny rule

# 9. Summary of Rules
sudo ufw status numbered
# Example:
# [ 1] 22/tcp  ALLOW IN  Anywhere
# [ 2] 23/tcp  DENY IN   Anywhere

# 10. Save and Push to GitHub
git init
git remote add origin https://github.com/Umxirrr/Task-4-Firewall-Configuration.git
git add .
git commit -m "Task 4 – Firewall Configuration and Testing"
git branch -M main
git push -u origin main
