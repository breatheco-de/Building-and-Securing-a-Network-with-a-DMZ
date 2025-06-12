
# DMZ Configuration Report with Cisco Packet Tracer

### 1. Lab Objective

> Briefly explain what was intended to be achieved with this lab.

**Example:**  
Configure a secure DMZ using a Cisco ISR router, applying NAT and ACLs to control traffic between LAN, DMZ, and the external network.


### 2. Implemented Topology

> Describe the network. You can include an image if the software allows it (Packet Tracer screenshot).

- Number of networks: __________
- Devices used: __________
- Brief description of the function of each zone (LAN, DMZ, External).

### 3. IP Addressing Plan

Complete the table with the assigned IPs (you can copy it from the statement if it hasn't changed).

| Device                  | IP              | Mask              | Gateway           |
|-------------------------|-----------------|-------------------|-------------------|
| PC_Internal             |                 |                   |                   |
| Server_DMZ              |                 |                   |                   |
| PC_External             |                 |                   |                   |
| Router_FW Gi0/0 (LAN)   |                 |                   |                   |
| Router_FW Gi0/1 (DMZ)   |                 |                   |                   |
| Router_FW Gi0/2 (Ext)   |                 |                   |                   |

### 4. Applied Configuration (Summary)

> Summarize the most relevant commands or steps you executed. Use text + code snippets as needed.

- Interfaces configured with `ip address`
- NAT:
```bash
ip nat inside source static 192.168.2.10 192.168.3.1
```
- ACLs:
```bash
access-list 101 permit tcp any host 192.168.3.1 eq 80
access-list 100 deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
```

### 5. Verifications Performed

> Describe the tests and their results. Include screenshots or command outputs if possible.

- `ping` from PC_Internal to the router: ✅
- Web access from PC_External: ✅
- Blocking access from DMZ to LAN: ✅

### 6. Conclusions and Recommendations

> What did you learn from this exercise? What would you improve?

**Example:**  
I learned to apply NAT and ACLs in a simulated environment. I recommend verifying basic connectivity before applying firewall rules, as an IP error can block everything.

### 7. Evidence Screenshots

> Attach here (or in an annexed PDF) the requested screenshots: pings, browser, `show` commands, etc.

