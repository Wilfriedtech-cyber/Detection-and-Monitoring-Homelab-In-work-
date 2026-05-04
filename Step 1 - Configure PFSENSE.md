# pfSense Configuration

## Review

You will need to install the pfSense ISO and create a virtual machine. All requirements can be found in the first repository.

The installation process is fairly straightforward, but remember to add the LAN interface to your home router interface so you can perform the initial configurations.

Once everything is set up, you should be able to access the pfSense web UI by navigating to your router's IP address in a browser.

<img width="1039" height="801" alt="image" src="https://github.com/user-attachments/assets/d2da4bd0-0eed-4d12-baf5-ba7d9ec3da76" />

Default credentials:
- **Username:** admin
- **Password:** pfsense

<img width="1038" height="802" alt="image" src="https://github.com/user-attachments/assets/c5f7c535-d5bb-4e8b-b6ad-2060a91414c3" />
<img width="1047" height="812" alt="image" src="https://github.com/user-attachments/assets/e13a753f-a706-4464-a621-302817bc212f" />
<img width="1670" height="914" alt="image" src="https://github.com/user-attachments/assets/fe7b2228-556a-4018-a630-a6a37abca468" />

Now repeat the same process for **OPT2**.

<img width="1030" height="799" alt="image" src="https://github.com/user-attachments/assets/b30f14ca-5578-4e84-aa1e-447bb65cfcc0" />
<img width="1034" height="794" alt="image" src="https://github.com/user-attachments/assets/7a5f0711-8ebb-4262-89af-116ee39a657c" />

Repeat the same steps for all remaining interfaces as well.

To give them internet access, you will need to add an open firewall rule allowing traffic to any destination. This is for initial configuration purposes only and will be secured once all machines are able to communicate with each other.

<img width="1038" height="810" alt="image" src="https://github.com/user-attachments/assets/8cd09543-ccf8-4be1-ac0f-41beb04d5e11" />
<img width="1026" height="798" alt="image" src="https://github.com/user-attachments/assets/e6eaa27f-4e7a-43e7-a710-e88234bc45cf" />

Once completed, you should have the following result.

<img width="739" height="444" alt="image" src="https://github.com/user-attachments/assets/d8d9ff3a-198e-4467-af7c-5248e6828b2b" />

Next, we will statically assign IP addresses to the Domain Controller and other devices.

<img width="1688" height="1109" alt="image" src="https://github.com/user-attachments/assets/fe379363-1886-4baf-b1f6-afe8f8596d8d" />
