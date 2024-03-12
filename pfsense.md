# pfSense: Network Segmentation and Firewall

## Installing the ISO File

Get the ISO file from: [https://www.pfsense.org/download/](https://www.pfsense.org/download/)

**Note**: if the downloaded file is a .gz file, you will need to extract it via 7zip

Once finished, store the file in a directory dedicated to ISO files (this will make things a lot more convenient)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled.png)

## Setting Up pfSense Virtual Machine

Create a new VM in VirtualBox

Set a name and select the ISO file from your selected directory

Select the type to BSD and version to FreeBSD (64-bit)

For hardware, I put:

2 GB of RAM (2048 MB)

1 CPU

20GB Virtual Hard Disk size

Make sure everything is correct and press finish

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%201.png)

Launch pfSense (Click on Start on VirtualBox)

Accept

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%202.png)

Install pfSense

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%203.png)

Use Auto (UFS)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%204.png)

Select Entire Disk

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%205.png)

Select MBR (DOS Partition)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%206.png)

Finish

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%207.png)

Commit

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%208.png)

pfSense will begin installing

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%209.png)

When finished**, do not reboot**, just power off the VM

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2010.png)

Now right click on pfSense > Settings > Storage and remove the ISO image (Blue button on the right, next to Optical Drive)

The only Storage Device should be the pfSense.vdi file

(Do not skip step: skipping this step resulted in a permanent loop of the pfSense installation process)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2011.png)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2012.png)

Now, we will configure the network adapters according to the topology

Head over to Network

Attach Adapter 1 to the NAT Network we configured earlier. Select SOC Network

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2013.png)

Enable Adapter 2 and set it as an Internal Network and name it Vnet2. Repeat for Adapter 3 and 4 accordingly.

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2014.png)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2015.png)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2016.png)

Press OK to apply all changes

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2017.png)

Now this is where things could get annoying. VirtualBox does not allow you to configure more than 4 Adapters via the GUI, so we have to use the command line for this

Before doing anything though, let’s make it so that we can use VirtualBox commands regardless of our present working directory in the command line

Search for **“Edit the system environment variables**” using the Windows search bar

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2018.png)

Click on **Environment Variables > Path,** and edit

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2019.png)

Select new, select the directory “**C:\Program Files\Oracle\VirtualBox**”

**Note:** (May vary depending on the your installation path of VirtualBox)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2020.png)

Click OK on all tabs to write the changes

Now we can use VirtualBox commands regardless of which directory we are in.

We will now add the 2 additional adapters to pfSense. 

Change to the directory of where your pfSense VM is located.

In my case, it is C:\Users\Walter\Desktop\VM\Security Operations Center\pfSense

We will create 2 additional network adapters, Vnet5 and Vnet6 on an internal network using the Intel PRO/1000 MT Desktop adapter like the other 4 adapters.

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2021.png)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2022.png)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2023.png)

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

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2024.png)

Start pfSense. We should see this now

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2025.png)

Done

Notice how there are only 2 interfaces. 

pfSense got assigned the IP 192.168.0.8 via DHCP 

We will need to set up the 5 additional adapters

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2026.png)

### Assigning Interfaces

Press 1

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2027.png)

VLANs should not be set up now so press n

Map the interfaces to their respective adapters:

**WAN:** em0 (Adapter 1) (assigned by default)

**LAN**: em1 (Adapter 2)

**OPT1**:  em2 (Adapter 3)

**OPT2**: em3 (Adapter 4)

**OPT3** :em4 (Adapter 5)

**OPT4**: em5 (Adapter 6)

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2028.png)

y to Proceed. Notice all the interfaces appear in pfSense but they still need an IP address assigned

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2029.png)

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

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2030.png)

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

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2031.png)

Adapter 3 is now there

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2032.png)

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

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2033.png)

Adapter 4 is now there

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2034.png)

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

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2035.png)

We should see all of our adapters with their assigned IPs now

![Untitled](pfSense%20Network%20Segmentation%20and%20Firewall%209bd49df1ea2e4ab7ab54e4e59d36f032/Untitled%2036.png)

We will now continue to the Security Onion setup
