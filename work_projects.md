---
layout: default
---

This page serves as a record of the Cybersecurity-related projects I have done as part of my employement. These projects are completed separate from my homelab configuration.

# SIEM - Wazuh
For practice as we were evaluating various hosted SIEM tools, I deployed a Wazuh instance in an Ubuntu Server 22.04 VM on one of our Proxmox hosts. After evaluating multiple platforms for a hosted solution, the CEO decided to go with my Wazuh instance instead. At this point I began deploying Wazuh agents to some of our client servers and making sure we were getting the data we needed.

### Syslog configuration
As many of our clients use Sonicwalls, I also configured Wazuh to ingest the logs from the Sonicwalls through syslog. For this, I set up the Wazuh server behind our proxy server and gave it a subdomain under our primary .com. I opened up the necessary port forwarding for the subdomain to pass the syslog traffic through. With this done, I also began work on ingesting the logs from our clients' Synology file servers. This was the first major ordeal as there were no Synology decoders or rules included with Wazuh. I spent nearly two weeks learning and testing until I finally had some working decoders/rules for the Synology logs. I am still trying to tweak and clean up these to provide better details and clarity.
