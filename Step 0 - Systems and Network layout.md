# System and Network Requirements

## Server

Picture
<img width="3024" height="4032" alt="IMG_0985" src="https://github.com/user-attachments/assets/eaf5ee84-9c57-4fc8-bec5-f4b2a1be9568" />

I used a Dell desktop with 64 GB of RAM and a 500 GB SSD, on which I installed VMware ESXi. You can use a different machine, however I would recommend having at least 64 GB of RAM and 500 GB of storage, as VMware ESXi alone took up almost 200 GB. This will ensure a smooth testing experience.

## Virtual Machines

You will need the following ISO files:
- Windows 10 64-bit ==> ( https://www.microsoft.com/software-download/windows10 )
- Windows Server 2022 or any other version ==> ( https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022 )
- Latest pfSense ==> ( https://www.pfsense.org/download/ )
- Latest Kali Linux ==> ( https://www.kali.org/get-kali/#kali-platforms )
- Latest Ubuntu Desktop ==> ( https://ubuntu.com/download/desktop )

The installation process for each virtual machine on VMware ESXi is fairly straightforward. I went with the default configurations for each machine until I reached the point of assigning storage and network groups.

After installing VMware ESXi, I proceeded to upload and install the virtual machines.

<img width="1309" height="803" alt="image" src="https://github.com/user-attachments/assets/0fbb5538-916b-47be-bf3c-89aff30c1b10" />

## Networking

I used a /29 subnet, which gives a subnet mask of **255.255.255.248**. The usable address pool ranges from **x.x.x.250 - x.x.x.254**, since the first address is reserved for the default gateway and the last for the broadcast address.

> **Tip:** You can reuse the same Ubuntu ISO to create two separate virtual machines — one for the vulnerable machine and one for the Splunk machine.

Every default gateway on each interface is connected to pfSense, with one additional interface connected to my home router. (See pfSense Configuration)

<img width="1895" height="899" alt="image" src="https://github.com/user-attachments/assets/5de2245d-3034-44f5-ab31-9be8d36068b1" />
<img width="1675" height="679" alt="image" src="https://github.com/user-attachments/assets/64569450-5c51-4a4d-a0a6-723f627261d8" />
