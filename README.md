# Security Operations Center & Pentesting Home Lab (Set Up)

## **Objective**

The goal of this lab is to learn cybersecurity in the lens of both the blue team and the red team (purple teaming). We will set up a purposefully weak environment via VirtualBox. Once the lab is set up, we can perform various attacks and gradually strengthen the security of the machines and network, giving us exposure and hands-on experience to a wide variety of tools in the process. This repository serves to document each individual step for troubleshooting and future reference.

**Blue Team**

We will use Ubuntu, Security Onion and Splunk to see alerts and logs created by the attacks and Active Directory. The goal is to strengthen the security posture of the entire network, practice efficient log aggregation and implement stronger firewall and IDS/IPS rules.

**Red Team**

We will use Kali Linux to perform attacks on the network, particularly the Active Directory environment. The goal is to find all possible attack vectors, vulnerabilities and use exploits to see what data we can collect and what damage we can cause. Additionally, we will try our best to evade detection from the blue team and bypass rules.

</br>

## **Topology**

<img src = "/images/Untitled.png" width = 100% height = 100%>

**NAT Network (192.168.0.xxx)**

pfSense will be the only VM attached to this adapter since it will act as the router within the virtualized environment. No machines in this lab should be able to communicate with systems outside of the network (Host VM, Internet, etc). The VMs will be able to communicate with each other via pfSense and multiple internal networks (”Vnets”)

**Internal Network (Vnet2 - 192.168.1.xxx)**

This will act as the LAN. A Kali Linux VM will be attached to this adapter to simulate an attacker/ red teamer

**Internal Network (Vnet3 - 192.168.2.xxx)**

This will connect the Active Directory (AD) environment to pfSense. Additional machines can be added to this subnet in the future, but for now we want the victim network to be comprised of Windows machines running on AD.

**Internal Network (Vnet4 - 192.168.3.xxx)**

This will connect the mini security operations center (SOC) to pfSense. This subnet consists of a Security Onion server and an analyst VM running Ubuntu to access Security Onion via web interface.

**Internal Network (Vnet5)**

This adapter is dedicated to mirror traffic from the victim network to the SOC for analysis.

**Internal Network (Vnet6 - 192.168.4.xxx)**

This will connect Splunk/ Ubuntu Server to pfSense. Splunk receives logs from the victim network via universal forwarder. 

</br>

## Hardware

A home lab like this where multiple virtual machines will be saved, deployed and running will require the host PC to have a very strong CPU and sufficient RAM and storage. 

**Note**: It might have been a better idea to run this lab on the cloud, but I wanted to have full control over the environment and learn how to set things up on my own. I plan on building a similar lab on the cloud for the future.

</br>

For reference, the build I used during this lab was:

**CPU**: Intel Core i7 14700k (20 cores 28 threads)

**Memory**: 32GB

**Storage**: 2TB SSD

The performance was exceptionally good, I had no problems.

</br>

## Set Up

I am running this lab on Oracle VM VirtualBox.

Before starting, we need to create a NAT Network within our virtualized environment

Navigate to File > Tools > Network Manager

<img src = "/images/Untitled 1.png" width = 60% height = 60%>

Select the NAT Networks tab and Press Create

I named mine SOC Network

I set the prefix to 192.168.0.0/24

Enable DHCP

Leave IPv6 disabled for now

<img src = "/images/Untitled 2.png" width = 60% height = 60%>

</br>

## Chapters

[pfSense: Network Segmentation and Firewall](SOC%20920d37ca2fe44379a9c51eebbfc97047/pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032.md)

[Security Onion: All-in-One Security Monitoring, Log Management, and IDS System](SOC%20920d37ca2fe44379a9c51eebbfc97047/Security%20Onion%20All-in-One%20Security%20Monitoring,%20Log%20f675c2a3a508456c8aecb5655e17a5f7.md)

[Ubuntu: Security Onion Management](SOC%20920d37ca2fe44379a9c51eebbfc97047/Ubuntu%20Security%20Onion%20Management%2085b9f6496cea49e7a93312019d626acd.md)

[Kali Linux: Attack Box](SOC%20920d37ca2fe44379a9c51eebbfc97047/Kali%20Linux%20Attack%20Box%207a30005ad983440f8ab8cd6cc7c13e30.md)

[pfSense: Configuring Interfaces and Rules](SOC%20920d37ca2fe44379a9c51eebbfc97047/pfSense%20Configuring%20Interfaces%20and%20Rules%205bb7d11fa79f482598ee96b582a45d2b.md)

[Active Directory: Domain Controller Setup](SOC%20920d37ca2fe44379a9c51eebbfc97047/Active%20Directory%20Domain%20Controller%20Setup%2043f1ccba8fdb4ec6a0c6694324cbe0c0.md)

[Active Directory: Windows 10 Client Setup](SOC%20920d37ca2fe44379a9c51eebbfc97047/Active%20Directory%20Windows%2010%20Client%20Setup%2058fbf006a77742da83e68c3f6ea32235.md)

[Splunk Setup on Ubuntu Server](SOC%20920d37ca2fe44379a9c51eebbfc97047/Splunk%20Setup%20on%20Ubuntu%20Server%201cf095f706ee42a89fa228cc0bf2cfa7.md)

[Forwarding AD Logs to Splunk](SOC%20920d37ca2fe44379a9c51eebbfc97047/Forwarding%20AD%20Logs%20to%20Splunk%201ece17d5415c4ff4bf0b86e94e205bd6.md)


## Completion 

Our lab is finally setup, and we can begin attacking and collecting logs.

Keep in mind that we set the worst security configurations possible, so there’s a lot of things we can do with this lab. There’s a lot of tools we can use and play around with, and a lot of fixes that need to be implemented.

For starters, we can just do a simple nmap scan and see what ports and services are open on the DC. From there, we can use something like Metasploit to begin attacking the AD network. 

<img src = "/images/Untitled 3.png" width = 60% height = 60%>

## Additional Notes

1. pfSense must be running at all times when this lab is being used.

2. When launching Security Onion, you may have to wait around 10 minutes for all the services to be running (important for log collection)

Run sudo so-status upon boot

<img src = "/images/Untitled 4.png" width = 60% height = 60%>

Run again after a few minutes to see if the services are running

<img src = "/images/Untitled 5.png" width = 60% height = 60%>
