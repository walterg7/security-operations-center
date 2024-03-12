# Active Directory: Domain Controller Setup

We will use the latest Windows Server version (2022) as the Domain Controller and have one Windows 10 Client for now

The Windows Server 2022 ISO can be downloaded here: [https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)

I chose the English 64-bit ISO Download

Name the VM

I gave it 2GB (2048) of RAM

2 CPUs

50GB Virtual Disk

<img src = "/images/domaincontroller/Untitled.png" width = 60% height = 60%>

Attach Adapter 1 to Vnet3 (192.168.2.0/24)

<img src = "/images/domaincontroller/Untitled 1.png" width = 60% height = 60%>

Launch the VM

Choose Windows Server 2022 Standard Evaluation (Desktop Experience)

<img src = "/images/domaincontroller/Untitled 2.png" width = 60% height = 60%>

Accept the license

<img src = "/images/domaincontroller/Untitled 3.png" width = 60% height = 60%>

Choose Custom Install

<img src = "/images/domaincontroller/Untitled 4.png" width = 60% height = 60%>

Select Drive 0

<img src = "/images/domaincontroller/Untitled 5.png" width = 60% height = 60%>

OK

<img src = "/images/domaincontroller/Untitled 6.png" width = 60% height = 60%>

Install the OS on Drive 0 Partition 2 (50GB)

<img src = "/images/domaincontroller/Untitled 7.png" width = 60% height = 60%>

The install process will begin. It shouldn’t take too long

<img src = "/images/domaincontroller/Untitled 8.png" width = 60% height = 60%>

Enter a password and take note of it

Click on Finish

<img src = "/images/domaincontroller/Untitled 9.png" width = 60% height = 60%>

We should now see the login screen 

Go to Input > Keyboard > Send Ctrl+Alt+Dlt to log in

<img src = "/images/domaincontroller/Untitled 10.png" width = 60% height = 60%>

Once we’re in, head over to Windows 10 Button > Settings > System > About

Rename the system to something like DomainController

The VM will have to restart

<img src = "/images/domaincontroller/Untitled 11.png" width = 60% height = 60%>

Log in again, and head to the server manager dashboard

It should automatically open once we boot up

If not, look for Server Manager in the search bar

Click on Manage > Add Roles and Features

<img src = "/images/domaincontroller/Untitled 12.png" width = 60% height = 60%>

Leave everything at default settings until we get to Server Roles

<img src = "/images/domaincontroller/Untitled 13.png" width = 60% height = 60%>

Check Active Directory Domain Services

<img src = "/images/domaincontroller/Untitled 14.png" width = 60% height = 60%>

Check the Include management tolls box and click Add features

<img src = "/images/domaincontroller/Untitled 15.png" width = 60% height = 60%>

Click install

<img src = "/images/domaincontroller/Untitled 16.png" width = 60% height = 60%>

It shouldn’t take too long, close when finished

<img src = "/images/domaincontroller/Untitled 17.png" width = 60% height = 60%>

Notice the warning sign next to Manage (top left)

<img src = "/images/domaincontroller/Untitled 18.png" width = 60% height = 60%>

Click on the sign

We need to promote the VM to DC

Click on Promote this server to a domain controller

<img src = "/images/domaincontroller/Untitled 19.png" width = 60% height = 60%>

Select Add a new forest

Add a domain name (waltersdomain.com in my case)

Next

<img src = "/images/domaincontroller/Untitled 20.png" width = 60% height = 60%>

Leave the forest and domain functional levels at the default (Windows Server 2016)

Make sure DNS server and Global Catalog (GC) are checked

Set a DSRM password. Take note of it just in case

Next

<img src = "/images/domaincontroller/Untitled 21.png" width = 60% height = 60%>

Set a NetBIOS domain name (I just put my name)

Next

<img src = "/images/domaincontroller/Untitled 22.png" width = 60% height = 60%>

Leave at default settings

Next

<img src = "/images/domaincontroller/Untitled 23.png" width = 60% height = 60%>

Make sure all the settings are correct to pass the prerequisite check

Next

<img src = "/images/domaincontroller/Untitled 24.png" width = 60% height = 60%>

Install. The VM will automatically restart when finished

<img src = "/images/domaincontroller/Untitled 25.png" width = 60% height = 60%>

Once we’re back in, head back to the server manager, Manage > Add Roles and Features

<img src = "/images/domaincontroller/Untitled 26.png" width = 60% height = 60%>

Click Next (leave default settings) until you get to Server Roles

Check Active Directory Certificate Services

Next

<img src = "/images/domaincontroller/Untitled 27.png" width = 60% height = 60%>

Make sure Include management tools is checked

Add Features

<img src = "/images/domaincontroller/Untitled 28.png" width = 60% height = 60%>

Active Directory Certificate Services should be checked off now

Next

<img src = "/images/domaincontroller/Untitled 29.png" width = 60% height = 60%>

Click Next (leave default settings) until we get to confirmation

Install and restart

<img src = "/images/domaincontroller/Untitled 30.png" width = 60% height = 60%>

Close

<img src = "/images/domaincontroller/Untitled 31.png" width = 60% height = 60%>

When we’re back in the server dashboard, we should see the warning sign again

Click on Configure Active Directory Certificate Services

<img src = "/images/domaincontroller/Untitled 32.png" width = 60% height = 60%>

Next (Credentials should automatically be NetBIOSName\Administrator)

<img src = "/images/domaincontroller/Untitled 33.png" width = 60% height = 60%>

Check Certification Authority 

Next

<img src = "/images/domaincontroller/Untitled 34.png" width = 60% height = 60%>

Set the validity period to 99 years

<img src = "/images/domaincontroller/Untitled 35.png" width = 60% height = 60%>

Confirm the settings then click on Configure

<img src = "/images/domaincontroller/Untitled 36.png" width = 60% height = 60%>

Configure should succeed. Close

Once again, restart for the changes to take effect

<img src = "/images/domaincontroller/Untitled 37.png" width = 60% height = 60%>

When we’re back in the server manager, click on Tools > AD Users and Computers

<img src = "/images/domaincontroller/Untitled 38.png" width = 60% height = 60%>

On waltersdomain.com, right click on Users, New > User

<img src = "/images/domaincontroller/Untitled 39.png" width = 60% height = 60%>

We will add a new user for our Windows 10 Client

Set a name and login naming scheme (firstname.lastname is the most common)

<img src = "/images/domaincontroller/Untitled 40.png" width = 60% height = 60%>

Enter a password

For now, set it so that it never expires

Next

<img src = "/images/domaincontroller/Untitled 41.png" width = 60% height = 60%>

Confirm the settings and click on Finish

<img src = "/images/domaincontroller/Untitled 42.png" width = 60% height = 60%>

Search for Windows Defender Firewall on the search bar 

Turn everything off (remember we want the weakest security configurations possible for this lab. The point is to break things then fix them to make them stronger)

<img src = "/images/domaincontroller/Untitled 43.png" width = 60% height = 60%>

Make sure  every firewall is off

<img src = "/images/domaincontroller/Untitled 44.png" width = 60% height = 60%>

On the task bar at the bottom right, right click on the Internet icon and select Open Network & Internet Settings

Click on Change adapter options

Right click on Ethernet 2 > Properties > Double Click IPv4 Properties

Set an IP for the DC

I set it to 192.168.2.10

When you click on subnet mask, it should autofill to 255.255.255.0

Set the default gateway to 192.168.2.1

Set the DNS to 192.168.2.1

Click OK to confirm the settings

<img src = "/images/domaincontroller/Untitled 45.png" width = 60% height = 60%>

In the command prompt, type ipconfig /all to ensure the settings changed

Notice the Host Name, DNS suffix, IPv4, and Default Gateway

Our DC is successfully configured

<img src = "/images/domaincontroller/Untitled 46.png" width = 80% height = 80%>

**Next**: Setting up a Windows 10 AD Client
