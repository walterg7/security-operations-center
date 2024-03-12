# pfSense: Network Segmentation and Firewall

## Installing the ISO File

Get the ISO file from: [https://www.pfsense.org/download/](https://www.pfsense.org/download/)

**Note**: if the downloaded file is a .gz file, you will need to extract it via 7zip

Once finished, store the file in a directory dedicated to ISO files (this will make things a lot more convenient)

<img src = "/images/pfsense/Untitled.png" width = 60% height = 60%>

## Setting Up pfSense Virtual Machine

Create a new VM in VirtualBox

Set a name and select the ISO file from your selected directory

Select the type to BSD and version to FreeBSD (64-bit)

For hardware, I put:

2 GB of RAM (2048 MB)

1 CPU

20GB Virtual Hard Disk size

Make sure everything is correct and press finish

<img src = "/images/pfsense/Untitled 1.png" width = 60% height = 60%>

Launch pfSense (Click on Start on VirtualBox)

Accept

<img src = "/images/pfsense/Untitled 2.png" width = 60% height = 60%>

Install pfSense

<img src = "/images/pfsense/Untitled 3.png" width = 60% height = 60%>

Use Auto (UFS)

<img src = "/images/pfsense/Untitled 4.png" width = 60% height = 60%>

Select Entire Disk

<img src = "/images/pfsense/Untitled 5.png" width = 60% height = 60%>

Select MBR (DOS Partition)

<img src = "/images/pfsense/Untitled 6.png" width = 60% height = 60%>

Finish

<img src = "/images/pfsense/Untitled 7.png" width = 60% height = 60%>

Commit

<img src = "/images/pfsense/Untitled 8.png" width = 60% height = 60%>

pfSense will begin installing

<img src = "/images/pfsense/Untitled 9.png" width = 60% height = 60%>

When finished**, do not reboot**, just power off the VM

<img src = "/images/pfsense/Untitled 10.png" width = 60% height = 60%>

Now right click on pfSense > Settings > Storage and remove the ISO image (Blue button on the right, next to Optical Drive)

The only Storage Device should be the pfSense.vdi file

(Do not skip step: skipping this step resulted in a permanent loop of the pfSense installation process)

<img src = "/images/pfsense/Untitled 11.png" width = 60% height = 60%>

<img src = "/images/pfsense/Untitled 12.png" width = 60% height = 60%>

Now, we will configure the network adapters according to the topology

Head over to Network

Attach Adapter 1 to the NAT Network we configured earlier. Select SOC Network

<img src = "/images/pfsense/Untitled 13.png" width = 60% height = 60%>

Enable Adapter 2 and set it as an Internal Network and name it Vnet2. Repeat for Adapter 3 and 4 accordingly.

<img src = "/images/pfsense/Untitled 14.png" width = 60% height = 60%>

<img src = "/images/pfsense/Untitled 15.png" width = 60% height = 60%>

<img src = "/images/pfsense/Untitled 16.png" width = 60% height = 60%>

Press OK to apply all changes

<img src = "/images/pfsense/Untitled 17.png" width = 60% height = 60%>

Now this is where things could get annoying. VirtualBox does not allow you to configure more than 4 Adapters via the GUI, so we have to use the command line for this

Before doing anything though, let’s make it so that we can use VirtualBox commands regardless of our present working directory in the command line

Search for **“Edit the system environment variables**” using the Windows search bar

<img src = "/images/pfsense/Untitled 18.png" width = 60% height = 60%>

Click on **Environment Variables > Path,** and edit

<img src = "/images/pfsense/Untitled 19.png" width = 60% height = 60%>

Select new, select the directory “**C:\Program Files\Oracle\VirtualBox**”

**Note:** (May vary depending on the your installation path of VirtualBox)

<img src = "/images/pfsense/Untitled 20.png" width = 60% height = 60%>

Click OK on all tabs to write the changes

Now we can use VirtualBox commands regardless of which directory we are in.

We will now add the 2 additional adapters to pfSense. 

Change to the directory of where your pfSense VM is located.

In my case, it is C:\Users\Walter\Desktop\VM\Security Operations Center\pfSense

We will create 2 additional network adapters, Vnet5 and Vnet6 on an internal network using the Intel PRO/1000 MT Desktop adapter like the other 4 adapters.

<img src = "/images/pfsense/Untitled 21.png" width = 60% height = 60%>

<img src = "/images/pfsense/Untitled 22.png" width = 60% height = 60%>

<img src = "/images/pfsense/Untitled 23.png" width = 60% height = 60%>

```cpp
VBoxManage modifyvm "pfSense" --nic5 intnet
VBoxManage modifyvm "pfSense" --nictype5 82540EM
VBoxManage modifyvm "pfSense" --intnet5 "Vnet5"
VBoxManage modifyvm "pfSense" --cableconnected5 on

VBoxManage modifyvm "pfSense" --nic6 intnet
VBoxManage modifyvm "pfSense" --nictype6 82540EM
VBoxManage modifyvm "pfSense" --intnet6 "Vnet6"
VBoxManage modifyvm "pfSense" --cableconnected6 on
```

Now head over to VirtualBox

Notice that Adapters 5 and 6 show up under Network. You will not be able to modify these adapters using the GUI however, only using the command line like before. Only Adapters 1-4 can be modified within VirtualBox (kind of annoying but it’s whatever)

<img src = "/images/pfsense/Untitled 24.png" width = 60% height = 60%>

Start pfSense. We should see this now

<img src = "/images/pfsense/Untitled 25.png" width = 60% height = 60%>

Done

Notice how there are only 2 interfaces. 

pfSense got assigned the IP 192.168.0.8 via DHCP 

We will need to set up the 5 additional adapters

<img src = "/images/pfsense/Untitled 26.png" width = 60% height = 60%>

### Assigning Interfaces

Press 1

<img src = "/images/pfsense/Untitled 27.png" width = 60% height = 60%>

VLANs should not be set up now so press n

Map the interfaces to their respective adapters:

**WAN:** em0 (Adapter 1) (assigned by default)

**LAN**: em1 (Adapter 2)

**OPT1**:  em2 (Adapter 3)

**OPT2**: em3 (Adapter 4)

**OPT3** :em4 (Adapter 5)

**OPT4**: em5 (Adapter 6)

<img src = "/images/pfsense/Untitled 28.png" width = 60% height = 60%>

y to Proceed. Notice all the interfaces appear in pfSense but they still need an IP address assigned

<img src = "/images/pfsense/Untitled 29.png" width = 60% height = 60%>

### Assigning IPs

**LAN Interface (Adapter 2)**

The process is as follows:

Press 2 to set an IP address to the interface

Press 2 to change LAN

Do not configure IP via DHCP. We want to assign the IP ourselves.

Set IPv4 to 192.168.1.1

192.168.1.1 is going to be used to access the pfSense firewall via the WebGUI

Set subnet to 24

For LAN, press <ENTER> for none

Do NOT configure IPv6 address via DHCP6. Press n and enter

Leave the IPv6 address empty. Press enter for none

Enable DHCP server for this adapter/ LAN

IPv4 client range: 192.168.1.11-192.168.1.200

Do not revert to HTTP

<img src = "/images/pfsense/Untitled 30.png" width = 60% height = 60%>

**OPT1 (Adapter 3)**

Press 2 to set an IP address to the interface

Press 3 to change OPT1

Do not configure IP via DHCP. We want to assign the IP ourselves.

Set IPv4 to 192.168.2.1 

Set subnet to 24

For LAN, press <ENTER> for none

Do not configure IPv6 address via DHCP6. Press n and enter

Leave the IPv6 address empty. Press enter for none

No DHCP server for this adapter 

Do not revert to HTTP

<img src = "/images/pfsense/Untitled 31.png" width = 60% height = 60%>

Adapter 3 is now there

<img src = "/images/pfsense/Untitled 32.png" width = 60% height = 60%>

**OPT2 (Adapter 4)**

Press 2 to set an IP address to the interface

Press 4 to change OPT2

Do not configure IP via DHCP. We want to assign the IP ourselves.

Set IPv4 to 192.168.3.1 

Set subnet to 24

For LAN, press <ENTER> for none

Do not configure IPv6 address via DHCP6. Press n and enter

Leave the IPv6 address empty. Press enter for none

No DHCP server for this adapter

Do not revert to HTTP

<img src = "/images/pfsense/Untitled 33.png" width = 60% height = 60%>

Adapter 4 is now there

<img src = "/images/pfsense/Untitled 34.png" width = 60% height = 60%>

**OPT3 (Adapter 5)**

Leave OPT3 without an IP since it is the SPAN Port

**OPT4 (Adapter 6)**

Press 2 to set an IP address to the interface

Press 6 to change OPT4

Do not configure IP via DHCP. We want to assign the IP ourselves.

Set IPv4 to 192.168.4.1 

Set subnet to 24

For LAN, press <ENTER> for none

Do not configure IPv6 address via DHCP6. Press n and enter

Leave the IPv6 address empty. Press enter for none

No DHCP server for this adapter

Do not revert to HTTP

<img src = "/images/pfsense/Untitled 35.png" width = 60% height = 60%>

We should see all of our adapters with their assigned IPs now

<img src = "/images/pfsense/Untitled 36.png" width = 60% height = 60%>

We will now continue to the Security Onion setup
