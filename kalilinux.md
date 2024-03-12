# Kali Linux: Attack Box

We will be using a pre-built Kali box, not an ISO image. 

Get Kali from: [https://www.kali.org/get-kali/#kali-virtual-machines](https://www.kali.org/get-kali/#kali-virtual-machines)

Select 64-bit VirtualBox

**Note**: The download may be in a zip archive. You will need 7Zip to unzip it

In VirtualBox, press Add, and select the Kali VirtualBox file from the directory you put it in

It should be named: kali-linux-2023.4-virtualbox-amd64-1.16

<img src = "/images/kali/Untitled.png" width = 60% height = 60%>

Set only 1 adapter (Vnet2/ 192.168.1.xxx)

<img src = "/images/kali/Untitled 1.png" width = 60% height = 60%>

Start the VM and wait for it to boot

<img src = "/images/kali/Untitled 2.png" width = 60% height = 60%>

Enter the default credentials

User: kali

Password: kali

<img src = "/images/kali/Untitled 3.png" width = 60% height = 60%>

Done

<img src = "/images/kali/Untitled 4.png" width = 60% height = 60%>

Run ifconfig. This VM should be in the 192.168.1.0/24 subnet

This machine has an IP of 192.168.1.13

<img src = "/images/kali/Untitled 5.png" width = 60% height = 60%>

You can change the password if needed by running the passwd command

<img src = "/images/kali/Untitled 6.png" width = 60% height = 60%>

Next: Setting up pfSense Firewall from Kali
