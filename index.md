---
layout: default
---

![Cybersecurity](./images/hacker-8018474_640.png)

Welcome to my project site for my Cybersecurity Lab. This site is to document how my lab is set up and what projects I have been doing in the lab. I also have [this page](./work_projects.md) which covers cybersecurity-related projects I have completed at my current job.
<br />

# Learning Objectives
My plan with this lab setup is to practice what I learned in the Google Cybersecurity Professional course and what I've been learning on my own. I will be combining this will some HackTheBox practice as well, but as I am more interested in Blue Team practice at this time, I will primarily be focused on this lab.

Some of the main focal points currently are:
- to expand my knowledge of Wazuh and experiment with various integrations
- practice writing more custom decoders and rules for Wazuh
- implement and test more opensource security platforms
- practice Windows Domain management and security optimizations
- perform Red Team tests against the firewall
- perform Red Team tests to simulate an attacker who has gained access to the internal network
- potentially look at integrating AI-based solutions in the future
<br />

# Cybersecurity Lab Overview

## Hardware
The entire lab is currently running on a single Intel NUC I had retired some time ago from my homelab setup. The NUC is now just for testing purposes like this. The system is running Proxmox 8.2.4 at the moment. While this is a bit older processor it will still cover my needs for this lab until I can justify upgrading to a 3-node Proxmox cluster.
- Intel i7 7567U
- 32GB DDR4
- 500GB SATA SSD
<br />

## VMs
To simulate a "closed" network environment like a company would have, I have set up an OPNSense VM with the WAN connected to my network to provide it internet access. The LAN is a virtual switch under Proxmox and is the only network connection assigned to the other VMs. This let's me separate the lab environment from my main network and gives a way to simulate WAN-based attacks. I could have simply used VLANs to segment out the lab from my main network, but I wanted to have the ability to test against a firewall so as to be more realistic.
- OPNSense VM (Gateway & Firewall)
- Windows Server 2022 Standard Eval (Domain Controller & File Server)
- Windows 10 Professional (Domain Client A)
- Windows 11 Professional (Domain Client B)
- Ubuntu Server 22.04 (Wazuh SIEM)
- Kali Linux (This one will be used both on the external WAN side and internal LAN side to test vulnerabilities from both sides)

In the future I may move my Metasploitable VM into this network to create a very vulnerable client in the LAN. However for now, I want to focus on normal systems that would be used in a corporate environment.
<br />

### OPNSense
I'm sure to be questioned about why I went with OPNSense for the gateway/firewall element. Up till recently, I was using pfSense at home for my firewall. However, pfSense does not have a clean and easy-to-implement method for integrating with Wazuh or some other security-oriented services. OPNSense has a Wazuh plugin that adds it as a regular agent.

At work, we use Sonicwalls but I cannot justify paying for a physical Sonicwall or virtual appliance just for this lab. Also, Sonicwalls can only use the syslog method to export data to Wazuh. With OPNSense using an actual Wazuh agent, I can look at integrations where Wazuh can trigger an IP block against attacking IPs.
<br />

### Wazuh SIEM
There are a range of SIEM options out there, but I wanted something free and opensource. It's also the SIEM I implemented at my current job as I was tasked with learning more about cybersecurity practices. It has a nice feature set and decent popularity. The Wazuh team also has extensive blog posts with ways to expand on the base setup.

I initially tried to do the Wazuh install on Ubuntu Server 24.04, but the method of installing Wazuh on this version of Ubuntu was more complicated than the 22.04 installer script. I ended up having one issue after another and just decided to save time and go with 22.04 instead. Ran the easy Wazuh installation script and was up and running in no time.
<br />

### Windows Server & Domain
This one seemed like an obvious requirement. Larger companies are almost always going to have a domain. The security controls and logging that this would allow for is great not only for the cybersecurity context, but also to give me a chance to practice with management of a Windows domain. Of course I need some client PCs to make use of the domain, so I opted for both Windows 10 and Windows 11 clients. Windows 10 is still supported until Oct. 2025 so it is perfectly valid for my testing. Also, there are going to be companies still running Windows 10 up until the retirement date (and some beyond then). It also lets me see what differences there may be between Windows versions when implementing certain policies on the domain controller.

While I am focusing on the Windows-side more with the domain, I am considering using the LDAP functionality to integrate the Linux servers into the domain. This may be more common practice in larger corporations, but none of the clients I deal with at my current job use Linux on any servers. So this is more of a BONUS if I feel like I have time for it.
<br />



# Next Steps
[Part 2????](./part2.md)



<br />
<br />
<br />
<br />

----
Text can be **bold**, _italic_, ~~strikethrough~~ or `keyword`.
