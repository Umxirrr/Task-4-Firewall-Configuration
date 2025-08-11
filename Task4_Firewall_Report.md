# Task 4 – Firewall Configuration and Testing

## Objective
Configure the UFW firewall on Kali Linux to block incoming connections on port **23 (Telnet)** and verify from a remote system (Windows 11) that the port is inaccessible.

---

## Environment
- **Kali Linux** (VMware Workstation, IP: `192.168.101.130`)
- **Windows 11 Host** (Used for remote connection testing)

---

## Steps Performed

### 1. Enable UFW
```bash
sudo ufw enable
## 2. Block Port 23/TCP
  sudo ufw deny 23/tcp
Added firewall rule to deny all incoming traffic on TCP port 23.

## 3. Verify Firewall Rules
sudo ufw status numbered
Output:
Status: active

     To                         Action      From
[ 1] 23/tcp                     DENY IN     Anywhere
[ 2] 23/tcp (v6)                DENY IN     Anywhere (v6)

## 4. Start Listener on Port 23 in Kalit
sudo ncat -l 192.168.101.130 23
Started ncat to listen for incoming Telnet connections.

## 5. Test Connection from Windows 11
telnet 192.168.101.130 23
# Result:
Connecting To 192.168.101.130...Could not open connection to the host, on port 23: Connect failed
