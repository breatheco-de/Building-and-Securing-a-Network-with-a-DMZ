
# Demilitarized Zone (DMZ) Configuration with Cisco Router

Configure a Demilitarized Zone (DMZ) using a Cisco ISR router to host a web server, allowing controlled access from the external and internal networks, while isolating the internal network from the DMZ.

## Lab Topology

- **Central Router (Router_FW)**: Cisco ISR (e.g., 2911 or 4331)
    - GigabitEthernet0/0 (LAN) -> SW_Internal
    - GigabitEthernet0/1 (DMZ) -> SW_DMZ
    - GigabitEthernet0/2 (External) -> SW_External

- **Switches**: 3x Cisco 2960 (or 2960 IOS15)

- **End Devices**:
    - PC_Internal (on SW_Internal)
    - Server-PT Web_DMZ (on SW_DMZ)
    - PC_External (on SW_External)

## Step 1: IP Addressing Plan

### PC_Internal:
```
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: 0.0.0.0
```

### Server-PT Web_DMZ:
```
IP Address: 192.168.2.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.2.1
DNS Server: 0.0.0.0
```

### PC_External:
```
IP Address: 192.168.3.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.3.1
DNS Server: 0.0.0.0
```

---

## Step 2: Router Interface Configuration (Router_FW)

```bash
Router> enable
Router# configure terminal

Router_FW(config)# interface GigabitEthernet0/0
Router_FW(config-if)# ip address 192.168.1.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# interface GigabitEthernet0/1
Router_FW(config-if)# ip address 192.168.2.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# interface GigabitEthernet0/2
Router_FW(config-if)# ip address 192.168.3.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# end
Router_FW# write memory
```

## ✅ Step 3: Basic Connectivity Verification

Perform a `ping` from each device to its gateway. All should return `Replies`.

If it fails:
- Check IP, mask, and gateway.
- Use `show ip interface brief` on the router.
- Check switch ports (`show interface status`).
- Ensure cables are correct and connected (green indicators).

## Step 4: Static NAT Configuration on the Router

```bash
Router_FW(config)# interface GigabitEthernet0/1
Router_FW(config-if)# ip nat inside
Router_FW(config)# interface GigabitEthernet0/2
Router_FW(config-if)# ip nat outside
Router_FW(config)# ip nat inside source static 192.168.2.10 192.168.3.1
Router_FW# write memory
```

## Step 5: Enable Web Services on the DMZ Server

- Enable HTTP and HTTPS from the `Services` tab.
- (Optional) Customize `index.html`.

## Step 6: Initial Web Access Tests

From PC_External:
- Access `http://192.168.3.1`

From PC_Internal:
- Access `http://192.168.2.10`

## 🔒 Step 7: ACL Configuration for Security

```bash
Router_FW# configure terminal

! ACL 101 - traffic from external to DMZ
no access-list 101
ip access-list extended 101
10 permit icmp any any
20 permit tcp any host 192.168.3.1 eq 80
30 permit tcp any host 192.168.3.1 eq 443
exit

! ACL 100 - traffic from DMZ to LAN and Internet
ip access-list extended 100
10 permit icmp any 192.168.1.0 0.0.0.255 echo-reply
20 permit tcp any 192.168.1.0 0.0.0.255 established
30 permit tcp any 192.168.3.0 0.0.0.255 established
40 permit icmp any 192.168.3.0 0.0.0.255 echo-reply
50 deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
60 permit ip any any
exit

! Apply ACLs to interfaces
interface GigabitEthernet0/1
ip access-group 100 in
exit

interface GigabitEthernet0/2
ip access-group 101 in
exit

end
write memory
```

---

## 🔍 Step 8: Final Security Verification

From PC_External:
- `ping 192.168.3.1` → should work (by temporary rule)
- Browse to `http://192.168.3.1` → page should load

From PC_Internal:
- `ping 192.168.2.10` → should reply
- `telnet 192.168.2.10 80` → should connect

From Server-PT Web_DMZ:
- `ping 192.168.1.10` → should fail
- `telnet 192.168.1.10 80` → should fail

---

## 🛡️ Step 9: Best Practices (Remove ICMP in Production)

```bash
Router_FW# configure terminal
ip access-list extended 101
no 10
end
write memory
```

Verify that `ping` from PC_External to `192.168.3.1` now fails, but web access still works.

