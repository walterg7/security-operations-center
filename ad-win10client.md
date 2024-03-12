# Active Directory: Windows 10 Client Setup

Before starting, head back to the pfSense dashboard from Kali

Go to Services > DHCP Server > Network

Select the IP of the DC as the DNS (192.168.2.10)

<img src = "/images/win10client/Untitled.png" width = 60% height = 60%>

Enter the domain name that we set

Save and apply changes

<img src = "/images/win10client/Untitled 1.png" width = 60% height = 60%>

Note: We will need Windows 10 Enterprise edition in order for Active Directory to work. I learned the hard way that Windows 10 Home does not support AD

Link to Windows 10 Enterprise edition: [https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

Set a name and choose the correct ISO file

Skip unattended installation

<img src = "/images/win10client/Untitled 2.png" width = 60% height = 60%>

This VM has

2GB RAM

2 CPUs

50GB storage

Confirm the settings and finish

<img src = "/images/win10client/Untitled 3.png" width = 60% height = 60%>

Set Adapter 1 to Vnet3

<img src = "/images/win10client/Untitled 4.png" width = 60% height = 60%>

Start the VM, wait until you get to this menu

Next

<img src = "/images/win10client/Untitled 5.png" width = 60% height = 60%>

Accept the license

Next

<img src = "/images/win10client/Untitled 6.png" width = 60% height = 60%>

Choose custom install

<img src = "/images/win10client/Untitled 7.png" width = 60% height = 60%>

Select Drive 0 

Next

<img src = "/images/win10client/Untitled 8.png" width = 60% height = 60%>

Wait for the installation to finish (should take around 10 minutes)

<img src = "/images/win10client/Untitled 9.png" width = 60% height = 60%>

When we get to this menu, choose Domain Join instead (bottom left)

<img src = "/images/win10client/Untitled 10.png" width = 60% height = 60%>

Enter a name

<img src = "/images/win10client/Untitled 11.png" width = 60% height = 60%>

This is required, I just selected 3 random questions and put “me” as the answer

<img src = "/images/win10client/Untitled 12.png" width = 60% height = 60%>

We don’t need these, just disable all of them

<img src = "/images/win10client/Untitled 13.png" width = 60% height = 60%>

Not now

<img src = "/images/win10client/Untitled 14.png" width = 60% height = 60%>

When we’re in, the first thing we’re going to do is install guest additions so the experience is smoother (this lets us adjust the resolution of the VM without having black bars)

On top of the VM menu, click on Devices > Insert Guest Additions CD Image

<img src = "/images/win10client/Untitled 15.png" width = 60% height = 60%>

Head to the CD Drive and click on VBoxWindowsAdditions-amd64

<img src = "/images/win10client/Untitled 16.png" width = 60% height = 60%>

Go through the set up

<img src = "/images/win10client/Untitled 17.png" width = 60% height = 60%>

Install and reboot

<img src = "/images/win10client/Untitled 18.png" width = 60% height = 60%>

When we’re back in, go to Settings > System > About

Change the name and reboot again

<img src = "/images/win10client/Untitled 19.png" width = 60% height = 60%>

Click the monitor icon

Network and internet settings

<img src = "/images/win10client/Untitled 20.png" width = 60% height = 60%>

Change adapter options

<img src = "/images/win10client/Untitled 21.png" width = 60% height = 60%>

Right click Ethernet 2

Double Click on IPv4

Set a unique IP to the Client machine in the same subnet (192.168.2.xxx)

Subnet mask should autofill when you click on it

Default gateway is the pfSense em2 adapter (192.168.2.1)

Preferred DNS server is the DC (192.168.2.10)

<img src = "/images/win10client/Untitled 22.png" width = 60% height = 60%>

Go to cmd and enter ipconfig to make sure that the changes took place

<img src = "/images/win10client/Untitled 23.png" width = 60% height = 60%>

Go to Settings > Accounts

Click on connect

<img src = "/images/win10client/Untitled 24.png" width = 60% height = 60%>

Click on Join this device to a local Active Directory domain

<img src = "/images/win10client/Untitled 25.png" width = 60% height = 60%>

Enter the domain name (waltersdomain.com)

<img src = "/images/win10client/Untitled 26.png" width = 60% height = 60%>

Enter the credentials of the new user from earlier

<img src = "/images/win10client/Untitled 27.png" width = 60% height = 60%>

Restart

<img src = "/images/win10client/Untitled 28.png" width = 60% height = 60%>

We should see the NetBios\user name at the login screen

Enter the password

<img src = "/images/win10client/Untitled 29.png" width = 60% height = 60%>

“WALTERGUERREROPC” was too long (max is 15 characters)

A different naming scheme should probably be used

<img src = "/images/win10client/Untitled 30.png" width = 60% height = 60%>

**Next**: Setting up Splunk on Ubuntu Server
