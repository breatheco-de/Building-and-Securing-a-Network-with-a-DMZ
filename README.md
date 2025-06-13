<!-- hide -->
# Building and Securing a Network with a DMZ

> By [@vanemorocho](https://github.com/vanemorocho) and [other contributors](https://github.com/breatheco-de/commands-for-remote-hacking/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

*These instructions [are available in 🇪🇸 Spanish](https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/blob/main/README.es.md) :es:*
<!-- endhide -->

This lab is designed for students to acquire fundamental skills in defensive cybersecurity by configuring a Demilitarized Zone (DMZ) in Cisco Packet Tracer. The objectives are:

- Isolate critical services (DMZ)
- Control traffic using ACLs
- Expose web services in a controlled manner
- Secure NAT configuration

### ⚠️ Important Note for Students
This exercise is structured step by step to help you understand how to correctly and securely configure and protect a network with a DMZ. **It is very important that you follow the provided instructions precisely,** especially the IP addressing plan and the indicated commands.

   > Using other IPs or changing the configuration order may break connectivity, prevent NAT from working, or invalidate the ACLs.

*Later, you will be able to practice creating a free-form DMZ, designing your own topology and access rules. But in this lab, the goal is to first understand the logic and fundamentals by following a controlled model.*

## 🌱 How to start this project?

[Download the file here](https://github.com/breatheco-de/Building-and-Securing-a-Network-with-a-DMZ/raw/main/assets/DMZ_PROJECT.pka) and open it with Packet Tracer.

Once you have opened the file in Packet Tracer, you will see a floating window with instructions to follow.

## 📝 Instructions

At the start of this lab, **you do not need to create or cable the network from scratch**. A **prebuilt functional topology** is already provided in Packet Tracer so you can focus on what matters most: **security configuration**.

### Lab Topology

**Central Router (`Router_FW`): Cisco ISR 2911**

- `GigabitEthernet0/0` connected to `SW_Internal` (LAN network)  
- `GigabitEthernet0/1` connected to `SW_DMZ` (DMZ network)  
- `GigabitEthernet0/2` connected to `SW_External` (external/internet network)  

**Cisco 2960 Switches:**

- `SW_Internal` connects to `PC_Internal`  
- `SW_DMZ` connects to `Server-PT Web_DMZ`  
- `SW_External` connects to `PC_External`  

**End Devices:**

- `PC_Internal` (user in LAN)  
- `Server-PT Web_DMZ` (web server in the DMZ)  
- `PC_External` (external user simulating the internet)  

### What do you need to do?

Your task will be to **complete the logical configuration** of this prebuilt network. You must:

1. **Assign IP addresses** to all end devices and the router.  
   This ensures that each zone (LAN, DMZ, External) has basic connectivity.

2. **Configure static NAT** on the router so that the DMZ server can be accessed from outside.  
   > Using NAT is a key technique to hide private addresses and expose public services in a controlled way.

3. **Apply Access Control Lists (ACLs)** to restrict traffic between zones.  
   > ACLs simulate a firewall, blocking unauthorized access and allowing only what is necessary for each role.

4. **Perform functional validation tests**:
   - Pings from different points in the network
   - HTTP access from the external network to the server
   - Verify that certain accesses are **blocked**, such as attempts to connect from the DMZ to the LAN (INTERNAL_NETWORK)

These tests simulate real security situations, where you verify that only legitimate traffic is allowed and malicious or unnecessary traffic is blocked.

## 🚛 How to submit this project?

Once you have completed the Packet Tracer instructions, you must save your file and prepare a technical report following the official template provided [report template](https://github.com/breatheco-de/Building-and-Securing-a-Network-with-a-DMZ/blob/main/assets/report_DMZ.md). **Important!** Use the template as a guide to write your report. Submissions without structure or incomplete will not be accepted.

1. Create a public repository in your GitHub account named `dmz-lab` (or similar).
2. Upload the following files:
   - Your final Packet Tracer file.
   - `informe/Informe_DMZ_Laboratorio.md`: the completed report using the template.
   - `evidencias/`: screenshots of the tests performed.
3. Add a `README.md` that briefly explains the objective of the lab and the contents of the repository.
4. **Submit the repository link on the 4Geeks platform.**

<!-- hide -->
## Contributors

Thanks to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

1. [Vanessa Morocho (vanemorocho)](https://github.com/vanemorocho) contribution: (tutorial building) ✅, (documentation) 📖
  
2. [Alejandro Sanchez (alesanchezr)](https://github.com/alesanchezr), contribution: (bug reports) 🐛

This and many other exercises are created by students as part of the [Cybersecurity Bootcamp](https://4geeksacademy.com/us/coding-bootcamps/cybersecurity) at 4Geeks Academy by [Alejandro Sánchez](https://twitter.com/alesanchezr) and many other contributors. Discover more about our [Full Stack Developer Course](https://4geeksacademy.com/us/coding-bootcamps/part-time-full-stack-developer) and the [Data Science Bootcamp](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning).

<!-- endhide -->
