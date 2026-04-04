# System and Network Requirements
## Server
Picture
(STILLS NEEDS TO WORK ON)

I used a Dell desktop with 64 GB RAM and 500 SSD GB and I installed vmware esxi onto it. Of course you can use other machines but I would recommend to have a 64 gb ram and at least 500GB for storage as VMWARE ESXI By itself took almost 200 GB. If you would like a good testing experience.

## Virtual machines

you will need:
- Windows 10 64bit iso file ==> ( https://www.microsoft.com/software-download/windows10 )
- Windows server 2022 or (any other version) ==> ( https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022 )
- Latest pfsense iso file ==> ( https://www.pfsense.org/download/ )
- Latest Kali linux iso file ==> ( https://www.kali.org/get-kali/#kali-platforms )
- Latest Ubuntu desktop iso file ==> ( https://ubuntu.com/download/desktop )


They should be pretty straight forward when it comes to installing a virtual machine on vmware esxi and I basically went with the default configurations for each machines up until I have got to where I needed to assign storage and network group.


After I installed vmware ESXI, now was the time to upload the virtual machines and install them.

<img width="1309" height="803" alt="image" src="https://github.com/user-attachments/assets/0fbb5538-916b-47be-bf3c-89aff30c1b10" />

## Networking 

I used a /29 as the subnet mask will be **255.255.255.248**. So that means the adress pool should be between **x.x.x.250 - x.x.x.254**  because the first address is for the default gateway on that subnet and the last one is for the broadcast address.

Every default gateway on every interface would be connected to pfsense and one extra interface would be connected to my home router.( see Pfsense configuration )
