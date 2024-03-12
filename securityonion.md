# Security Onion: All-in-One Security Monitoring, Log Management, and IDS System

Download the Security Onion ISO from this GitHub repository: [https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md](https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md)

Version 2.3.280 (11/28/23)

Create a new VM

Set a name and select the ISO file from the right directory

Skip Unattended Installation

<img src = "/images/securityonion/Untitled.png" width = 60% height = 60%>

Security Onion recommends:

200 GB storage

12GB ram

4 CPUs

You may need to adjust these settings to accommodate your system hardware, but installation may take longer than normal.

Make sure everything is correct. Finish

<img src = "/images/securityonion/Untitled 1.png" width = 60% height = 60%>

Set the network adapters according to the topology

We should have 2 network adapters for this VM

<img src = "/images/securityonion/Untitled 2.png" width = 60% height = 60%>

Launch Security Onion

<img src = "/images/securityonion/Untitled 3.png" width = 60% height = 60%>

Type yes to continue

<img src = "/images/securityonion/Untitled 4.png" width = 60% height = 60%>

It will prompt you to enter an admin username and password. Take note of these 

(Note: When typing the password, the text will not show)

<img src = "/images/securityonion/Untitled 5.png" width = 60% height = 60%>

After that, package installation will begin (should take around 5 minutes)

<img src = "/images/securityonion/Untitled 6.png" width = 60% height = 60%>

Press enter

<img src = "/images/securityonion/Untitled 7.png" width = 60% height = 60%>

Login with the credentials you set earlier

You will be prompted to the Security Onion Setup 

<img src = "/images/securityonion/Untitled 8.png" width = 60% height = 60%>

Yes

<img src = "/images/securityonion/Untitled 9.png" width = 60% height = 60%>

Install

<img src = "/images/securityonion/Untitled 10.png" width = 60% height = 60%>

EVAL

<img src = "/images/securityonion/Untitled 11.png" width = 60% height = 60%>

Agree to the license terms

<img src = "/images/securityonion/Untitled 12.png" width = 60% height = 60%>

Set a host name. I left mine as securityonion

<img src = "/images/securityonion/Untitled 13.png" width = 60% height = 60%>

Use anyway

<img src = "/images/securityonion/Untitled 14.png" width = 60% height = 60%>

Vnet4 will be our management NIC

Make sure enp0s3 corresponds to the Vnet4 MAC address

<img src = "/images/securityonion/Untitled 15.png" width = 60% height = 60%>

<img src = "/images/securityonion/Untitled 16.png" width = 60% height = 60%>

Select static IP

<img src = "/images/securityonion/Untitled 17.png" width = 60% height = 60%>

Enter 192.168.3.10/24 (This will also be the IP to access it via web browser)

<img src = "/images/securityonion/Untitled 18.png" width = 60% height = 60%>

Set gateway to 192.168.3.1

<img src = "/images/securityonion/Untitled 19.png" width = 60% height = 60%>

Leave at default

<img src = "/images/securityonion/Untitled 20.png" width = 60% height = 60%>

Choose Airgap. This VM will have no access to the internet by default, and we would prefer to keep it that way for now.

<img src = "/images/securityonion/Untitled 21.png" width = 60% height = 60%>

Enter an email for the admin account (this does not have to be a real email, just make one up)

<img src = "/images/securityonion/Untitled 22.png" width = 60% height = 60%>

Enter a password

<img src = "/images/securityonion/Untitled 23.png" width = 60% height = 60%>

Choose IP

<img src = "/images/securityonion/Untitled 24.png" width = 60% height = 60%>

Yes

<img src = "/images/securityonion/Untitled 25.png" width = 60% height = 60%>

Leave at default

<img src = "/images/securityonion/Untitled 26.png" width = 60% height = 60%>

Select no for now, we will do this later when we set up Ubuntu

<img src = "/images/securityonion/Untitled 27.png" width = 60% height = 60%>

Confirm that all settings are correct

<img src = "/images/securityonion/Untitled 28.png" width = 60% height = 60%>

Select yes, and installation should begin (this could take around 40-60 minutes)

<img src = "/images/securityonion/Untitled 29.png" width = 60% height = 60%>

<img src = "/images/securityonion/Untitled 30.png" width = 60% height = 60%>

When finished, reboot.

!<img src = "/images/securityonion/Untitled 31.png" width = 60% height = 60%>

We will now move on to the Ubuntu (Analyst VM) setup
