# Forwarding AD Logs to Splunk

In the Splunk VM, click on Settings > Data > Forwarding and receiving

<img src = "/images/universal-forwarder/Untitled.png" width = 60% height = 60%>

Click on Configure receiving

<img src = "/images/universal-forwarder/Untitled 1.png" width = 60% height = 60%>

Click on New receiving port

<img src = "/images/universal-forwarder/Untitled 2.png" width = 60% height = 60%>

Enter port 9997 (Default port for universal forwarder)

Save

<img src = "/images/universal-forwarder/Untitled 3.png" width = 60% height = 60%>

Port 9997 should be enabled

<img src = "/images/universal-forwarder/Untitled 4.png" width = 60% height = 60%>

Go to Settings > Indexes

<img src = "/images/universal-forwarder/Untitled 5.png" width = 60% height = 60%>

Click New Index on the top right

Name wineventlog, leave everything else at default settings and save

<img src = "/images/universal-forwarder/Untitled 6.png" width = 60% height = 60%>

On DC go to, [https://www.splunk.com/en_us/download/universal-forwarder.html](https://www.splunk.com/en_us/download/universal-forwarder.html)

The DC may not have access to the Internet. If that is the case, follow these steps (these configurations also make the DC weaker for our future attacks)

From Kali, access the pfSense WebGUI

Select Rules from the Firewall dropdown and head to the Network tab

Add a new rule (first green button)

<img src = "/images/universal-forwarder/Untitled 7.png" width = 60% height = 60%>

Action: Pass

Protocol: Any

Source: Any

Destination: Any

<img src = "/images/universal-forwarder/Untitled 8.png" width = 60% height = 60%>

Save and apply the settings 

<img src = "/images/universal-forwarder/Untitled 9.png" width = 60% height = 60%>

Restart the DC and log back in. We should have access to the Internet

Use a web browser and sign in to Splunk ([https://www.splunk.com/en_us/download/universal-forwarder.html](https://www.splunk.com/en_us/download/universal-forwarder.html))

Select the 64-bit server option

<img src = "/images/universal-forwarder/Untitled 10.png" width = 60% height = 60%>

When it is finished downloading, open the Universal Forwarder setup

Accept the license

Select on-prem Splunk Enterprise instance

Next

<img src = "/images/universal-forwarder/Untitled 11.png" width = 60% height = 60%>

Enter credentials for the admin account credentials

<img src = "/images/universal-forwarder/Untitled 12.png" width = 60% height = 60%>

In the Splunk VM/ Ubuntu Server box enter ifconfig in the terminal.

<img src = "/images/universal-forwarder/Untitled 13.png" width = 60% height = 60%>

Use the IP of the Splunk VM (192.168.4.10)

Leave the default port 8089

<img src = "/images/universal-forwarder/Untitled 14.png" width = 60% height = 60%>

Same IP 

Enter port 9997

<img src = "/images/universal-forwarder/Untitled 15.png" width = 60% height = 60%>

Install

<img src = "/images/universal-forwarder/Untitled 16.png" width = 60% height = 60%>

Click finish when it’s done

<img src = "/images/universal-forwarder/Untitled 17.png" width = 60% height = 60%>

In the Splunk VM, go to Settings > Add Data

<img src = "/images/universal-forwarder/Untitled 18.png" width = 60% height = 60%>

Select forward (bottom right)

<img src = "/images/universal-forwarder/Untitled 19.png" width = 60% height = 60%>

The domain controller should be there by default (you might have to wait or refresh a few times for it to show up)

<img src = "/images/universal-forwarder/Untitled 20.png" width = 60% height = 60%>

Click on available hosts (WINDOWS - DC) so the DC is in Selected hosts.

Enter a server class name

Next

<img src = "/images/universal-forwarder/Untitled 21.png" width = 60% height = 60%>

For now, check every option for local event logs

Application

ForwardedEvents

Security

Setup

System

Next

<img src = "/images/universal-forwarder/Untitled 22.png" width = 60% height = 60%>

Select wineventlog as the index

We want this index to have all the logs from the DC

<img src = "/images/universal-forwarder/Untitled 23.png" width = 60% height = 60%>

Make sure the settings are correct

<img src = "/images/universal-forwarder/Untitled 24.png" width = 60% height = 60%>

Click on the wineventlog index

<img src = "/images/universal-forwarder/Untitled 25.png" width = 60% height = 60%>

To see if this works, log out of the DC or client machine and log back in

On Splunk, we should see some alerts generated

<img src = "/images/universal-forwarder/Untitled 26.png" width = 60% height = 60%>

We should also start seeing some logs from Security Onion

<img src = "/images/universal-forwarder/Untitled 27.png" width = 60% height = 60%>

<img src = "/images/universal-forwarder/Untitled 28.png" width = 60% height = 60%>

<img src = "/images/universal-forwarder/Untitled 29.png" width = 60% height = 60%>
