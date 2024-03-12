# pfSense: Configuring Interfaces and Rules

In Kali, head over to the pfSense web interface (192.168.1.1)

**Note**: pfSense must be running at all times during this lab

You should see this warning message, just proceed

Advanced > Accept Risk and Continue

<img src = "/images/firewall/Untitled.png" width = 60% height = 60%>

Enter the default pfSense credentials

Username: admin 

Password: pfsense

<img src = "/images/firewall/Untitled 1.png" width = 60% height = 60%>

We will have to go through the setup wizard first

Next

<img src = "/images/firewall/Untitled 2.png" width = 60% height = 60%>

Set primary DNS to 8.8.8.8

Secondary 4.4.4.4

<img src = "/images/firewall/Untitled 3.png" width = 60% height = 60%>

Leave time server hostname at default

Set the appropriate time zone

<img src = "/images/firewall/Untitled 4.png" width = 60% height = 60%>

Leave everything at default

WAN should have DHCP enabled by default

<img src = "/images/firewall/Untitled 5.png" width = 60% height = 60%>

**Optional step**

If you uncheck both options it will generate a lot alerts when we configure Suricata

<img src = "/images/firewall/Untitled 6.png" width = 60% height = 60%>

Leave LAN (Vnet2) at 192.168.1.1/24

Next

<img src = "/images/firewall/Untitled 7.png" width = 60% height = 60%>

Enter a new admin password, take note of it

<img src = "/images/firewall/Untitled 8.png" width = 60% height = 60%>

Reload

<img src = "/images/firewall/Untitled 9.png" width = 60% height = 60%>

Scroll down and press finish

<img src = "/images/firewall/Untitled 10.png" width = 60% height = 60%>

Accept the license. Our dashboard should look like this

<img src = "/images/firewall/Untitled 11.png" width = 60% height = 60%>

## Naming Interfaces

Go to Interfaces > Interface Assignments

<img src = "/images/firewall/Untitled 12.png" width = 60% height = 60%>

Click on LAN

You can leave the name to LAN or change it to Kali (leave everything else at default settings)

<img src = "/images/firewall/Untitled 13.png" width = 60% height = 60%>

Click save at the bottom and apply changes

<img src = "/images/firewall/Untitled 14.png" width = 60% height = 60%>

<img src = "/images/firewall/Untitled 15.png" width = 60% height = 60%>

Name OPT1: Network (This will be our Windows AD network)

You should probably name it something less generic

Save and apply changes

<img src = "/images/firewall/Untitled 16.png" width = 60% height = 60%>

Name OPT2: Security Onion

Save and Apply changes

<img src = "/images/firewall/Untitled 17.png" width = 60% height = 60%>

OPT3 is our SPAN Port

Enable it and name it 

Save and apply changes

<img src = "/images/firewall/Untitled 18.png" width = 60% height = 60%>

Name OPT4 Splunk

Save and apply changes 

<img src = "/images/firewall/Untitled 19.png" width = 60% height = 60%>

Our interfaces should now look like this

<img src = "/images/firewall/Untitled 20.png" width = 20% height = 20%>

Head over to Bridges 

<img src = "/images/firewall/Untitled 21.png" width = 60% height = 60%>

Go to Bridges > Select NETWORK from member interface dropdown

Display advanced options

Set span port to SPANPORT

<img src = "/images/firewall/Untitled 22.png" width = 60% height = 60%>

Scroll down and save

<img src = "/images/firewall/Untitled 23.png" width = 60% height = 60%>

To mass generate logs and alerts, we will enable traffic from all ports and protocols

We will change this later to see how much of an impact having this configuration will have on the network

Head over to Firewall > Rules

Click Add

<img src = "/images/firewall/Untitled 24.png" width = 60% height = 60%>

Set Protocol to any and save

<img src = "/images/firewall/Untitled 25.png" width = 60% height = 60%>

Apply changes

<img src = "/images/firewall/Untitled 26.png" width = 60% height = 60%>

**Next**: Building an Active Directory environment to simulate an enterprise network
