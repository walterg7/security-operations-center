# Splunk Setup on Ubuntu Server

Get the Ubuntu Server ISO from: [https://ubuntu.com/download/server](https://ubuntu.com/download/server)

Same process

Choose a name for the VM and select the right ISO file

Skip unattended installation

<img src = "/images/splunk/Untitled.png" width = 60% height = 60%>

I put 

4GB RAM 

2 CPUs 

100GB storage

Keep in mind our logs will be stored here as well

Confirm the settings and finish 

<img src = "/images/splunk/Untitled 1.png" width = 60% height = 60%>

To make things easier, we want to enable Internet connection during installation

Set Adapter 1 to the NAT Network

Set Adapter 2 to Vnet6 (192.168.4.xxx)

<img src = "/images/splunk/Untitled 2.png" width = 60% height = 60%>

Start the VM

Select the first option (Try or Install Ubuntu Server)

<img src = "/images/splunk/Untitled 3.png" width = 60% height = 60%>

English

<img src = "/images/splunk/Untitled 4.png" width = 60% height = 60%>

Continue without updating

<img src = "/images/splunk/Untitled 5.png" width = 60% height = 60%>

Done

<img src = "/images/splunk/Untitled 6.png" width = 60% height = 60%>

Choose Ubuntu server

Done

<img src = "/images/splunk/Untitled 7.png" width = 60% height = 60%>

Leave at default

<img src = "/images/splunk/Untitled 8.png" width = 60% height = 60%>

Leave empty

<img src = "/images/splunk/Untitled 9.png" width = 60% height = 60%>

Done

<img src = "/images/splunk/Untitled 10.png" width = 60% height = 60%>

Scroll down, done

<img src = "/images/splunk/Untitled 11.png" width = 60% height = 60%>

Done

<img src = "/images/splunk/Untitled 12.png" width = 60% height = 60%>

Continue

<img src = "/images/splunk/Untitled 13.png" width = 60% height = 60%>

Put a name, server name, username, and password

Done

<img src = "/images/splunk/Untitled 14.png" width = 60% height = 60%>

Skip for now, continue

<img src = "/images/splunk/Untitled 15.png" width = 60% height = 60%>

We can leave SSH install

Done

<img src = "/images/splunk/Untitled 16.png" width = 60% height = 60%>

We don’t need to install any of these for now

Done

<img src = "/images/splunk/Untitled 17.png" width = 60% height = 60%>

Install should begin (took around 10 minutes)

<img src = "/images/splunk/Untitled 18.png" width = 60% height = 60%>

Reboot now

<img src = "/images/splunk/Untitled 19.png" width = 60% height = 60%>

When we’re in, we will only see the terminal. We will install the Ubuntu GUI to make things easier

The reason we use Ubuntu Server over Ubuntu desktop, even though we want the GUI, is because this VM is dedicated to only using Splunk. We don’t need the extra packages and resources installed that come with desktop

<img src = "/images/splunk/Untitled 20.png" width = 60% height = 60%>

In the CLI, run sudo apt-get install ubuntu-desktop

When finished, reboot

Upon reboot we will see the GUI log in.

<img src = "/images/splunk/Untitled 21.png" width = 60% height = 60%>

Setting up VBox Guest Additions for a smoother experience

On top of the VM, click on Devices > Insert Guest Additions CD Image

In the terminal, run lsblk

cd into the /media/name/VBox_GAs

<img src = "/images/splunk/Untitled 22.png" width = 60% height = 60%>

Run the VBoxLinuxAdditions.run file

<img src = "/images/splunk/Untitled 23.png" width = 60% height = 60%>

If you haven’t already, sign up for a Splunk account and start the free trial for Splunk enterprise

<img src = "/images/splunk/Untitled 24.png" width = 60% height = 60%>

Confirm you account

<img src = "/images/splunk/Untitled 25.png" width = 60% height = 60%>

Head to Products > Platform > Splunk Enterprise 

Select the .tgz download for Ubuntu

<img src = "/images/splunk/Untitled 26.png" width = 60% height = 60%>

Extract using tar xvzf

<img src = "/images/splunk/Untitled 27.png" width = 60% height = 60%>

cd to splunk/bin (we can move the directory later)

Start Splunk by running ./splunk start

<img src = "/images/splunk/Untitled 28.png" width = 60% height = 60%>

Enter an admin username and password

<img src = "/images/splunk/Untitled 29.png" width = 60% height = 60%>

When finished, we could access splunk via 127.0.0.1:8000

<img src = "/images/splunk/Untitled 30.png" width = 60% height = 60%>

Log in using the credentials we set earlier

<img src = "/images/splunk/Untitled 31.png" width = 60% height = 60%>

We now have Splunk on Ubuntu Server (GUI)

<img src = "/images/splunk/Untitled 32.png" width = 60% height = 60%>

At this point, we can detach the VM from the NAT Network and leave only 1 adapter for Vnet6.

<img src = "/images/splunk/Untitled 33.png" width = 60% height = 60%>

When we’re back in, cd to /etc/netplan and edit the network config file (.yaml)

<img src = "/images/splunk/Untitled 34.png" width = 60% height = 60%>

Same process as earlier

Set IP to 192.168.4.10/24

Default gateway: 192.168.4.1

(ignore enp0s8)

<img src = "/images/splunk/Untitled 35.png" width = 60% height = 60%>

Run sudo netplan apply

Run ifconfig to confirm the changes took place

<img src = "/images/splunk/Untitled 36.png" width = 60% height = 60%>

**Next**: Setting up Universal Forwarder
