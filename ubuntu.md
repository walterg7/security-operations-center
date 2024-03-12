# Ubuntu: Security Onion Management

Get the Ubuntu Desktop (22.04.4) ISO from: [https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)

In VirtualBox, Create a new VM

I named the VM Ubuntu (Blue)

Select the ISO folder from the path

Make sure to Skip Unattended Installation

<img src = "/images/ubuntu/Untitled.png" width = 60% height = 60%>

4GB of RAM 

2 CPUs

25GB storage

Make sure everything is correct and press finish

<img src = "/images/ubuntu/Untitled 1.png" width = 60% height = 60%>

Right click the VM and go to Settings > Network to set the adapters according to our topology

It should only be attached to Vnet4

<img src = "/images/ubuntu/Untitled 2.png" width = 60% height = 60%>

Start the VM

Wait until you see this menu, and select install Ubuntu

<img src = "/images/ubuntu/Untitled 3.png" width = 60% height = 60%>

English

<img src = "/images/ubuntu/Untitled 4.png" width = 60% height = 60%>

Normal Installation

<img src = "/images/ubuntu/Untitled 5.png" width = 60% height = 60%>

Erase disk and install Ubuntu

Install now

<img src = "/images/ubuntu/Untitled 6.png" width = 60% height = 60%>

Continue

<img src = "/images/ubuntu/Untitled 7.png" width = 60% height = 60%>

Select time zone

<img src = "/images/ubuntu/Untitled 8.png" width = 60% height = 60%>

Set a name and computer name

I put securityonion-mgmt since that’s the purpose of this VM

Pick a username and password, keep note of these

Continue

<img src = "/images/ubuntu/Untitled 9.png" width = 60% height = 60%>

Installation should begin shortly

<img src = "/images/ubuntu/Untitled 10.png" width = 60% height = 60%>

When the installation finishes, restart and log in

<img src = "/images/ubuntu/Untitled 11.png" width = 60% height = 60%>

Once we’re back in open the terminal (Bottom left > Show Applications > Terminal)

(Right click and add to favorites so it is pinned on the taskbar)

Run ifconfig.

It will not work since net-tools is not installed so run 

sudo apt install net-tools

<img src = "/images/ubuntu/Untitled 12.png" width = 60% height = 60%>

Remember that there is no DHCP for Vnet4, so we will have to manually enter an IP.

In the terminal, cd /etc/netplan and edit the network manager file (.yaml)

Use a text editor of choice to edit the network config file

(**Note**: run ls to see the exact name of the .yaml file.)

<img src = "/images/ubuntu/Untitled 13.png" width = 60% height = 60%>

Make sure to set an IP in the SOC subnet (192.168.3.xxx) and set the gateway to 192.168.3.1 

Make sure everything is indented properly

Write changes and quit to terminal

<img src = "/images/ubuntu/Untitled 14.png" width = 60% height = 60%>

Run sudo netplan apply

Run ifconfig to make sure the changes took place

<img src = "/images/ubuntu/Untitled 15.png" width = 60% height = 60%>

Head back to Security Onion. We will assign this Ubuntu machine the analyst role

Log in and run sudo so-allow

Select a, then enter the IP of the Ubuntu machine (192.168.3.11)

<img src = "/images/ubuntu/Untitled 16.png" width = 60% height = 60%>

We should see this message when the analyst role has been successfully added

<img src = "/images/ubuntu/Untitled 17.png" width = 60% height = 60%>

Head back to the Ubuntu VM and go to the Security Onion web interface (192.168.3.10)

There will be a security alert by default but just proceed (Advanced > Accept the Risk and Continue)

<img src = "/images/ubuntu/Untitled 18.png" width = 60% height = 60%>

Enter the credentials we set earlier during the Security Onion setup

<img src = "/images/ubuntu/Untitled 19.png" width = 60% height = 60%>

We should see the dashboard when we successfully log in

<img src = "/images/ubuntu/Untitled 21.png" width = 60% height = 60%>

Notice the admin user

<img src = "/images/ubuntu/Untitled 22.png" width = 60% height = 60%>

Security Onion and Security Onion Management (Ubuntu) have been configured successfully

<img src = "/images/ubuntu/Untitled 23.png" width = 60% height = 60%>

Next, we will install a Kali Linux VM and configure pfSense from there

</br>

**Troubleshooting**

I was unable to ping Security Onion (192.168.3.10) from the Ubuntu VM. I added these firewall rules to fix the problem (This is after Kali was set up)

<img src = "/images/ubuntu/Untitled 24.png" width = 60% height = 60%>

<img src = "/images/ubuntu/Untitled 25.png" width = 60% height = 60%>

Pinging and connecting to 192.168.3.0/24 should now work

<img src = "/images/ubuntu/Untitled 26.png" width = 60% height = 60%>

<img src = "/images/ubuntu/Untitled 27.png" width = 60% height = 60%>
