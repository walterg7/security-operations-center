# Security Operations Center & Pentesting Home Lab (Set Up)

## **Objective**

The goal of this lab is to learn cybersecurity in the lens of both the blue team and the red team (purple teaming). We will set up a purposefully weak environment via VirtualBox. 
We will use the following:
- pfSense router for network segmentation and firewall
- Security Onion and Splunk for our SIEM + IDS/IPS
- An Active Directory environment to simulate an enterprise network
- A Kali Linux machine to simulate an attacker/ pentester

 Once the lab is set up, we can perform various attacks and gradually strengthen the security of the machines and network, giving us exposure and hands-on experience to a wide variety of tools in the process. This repository serves to document each individual step for troubleshooting and future reference.

**Blue Team**

We will use Ubuntu, Security Onion and Splunk to see alerts and logs created by the attacks and Active Directory. The goal is to strengthen the security posture of the entire network, practice efficient log aggregation and implement stronger firewall and IDS/IPS rules.

**Red Team**

We will use Kali Linux to perform attacks on the network, particularly the Active Directory environment. The goal is to find all possible attack vectors, vulnerabilities and use exploits to see what data we can collect and what damage we can cause. Additionally, we will try our best to bypass rules and evade detection from the blue team.

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

### - [pfSense: Network Segmentation and Firewall](pfsense.md)

### - [Security Onion: All-in-One Security Monitoring, Log Management, and IDS System](securityonion.md)

Ubuntu: Security Onion Management

Kali Linux: Attack Box

pfSense: Configuring Interfaces and Rules

Active Directory: Domain Controller Setup

Active Directory: Windows 10 Client Setup

Splunk Setup on Ubuntu Server

Forwarding AD Logs to Splunk


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
