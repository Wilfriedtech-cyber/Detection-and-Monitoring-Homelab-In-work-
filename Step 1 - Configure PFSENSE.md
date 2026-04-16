# Review

You will need to install the iso for pfsense and create a virtual machine. I have all the requirements in the first repository.
The installation process should be straight forward but remember to add the LAN interface to your home router interface so you can do the initial configurations.

when everything is done, you should be able to see this page by going to your browser and looking for your router ip address
<img width="1039" height="801" alt="image" src="https://github.com/user-attachments/assets/d2da4bd0-0eed-4d12-baf5-ba7d9ec3da76" />
username: Admin

psswd:  pfsense

<img width="1038" height="802" alt="image" src="https://github.com/user-attachments/assets/c5f7c535-d5bb-4e8b-b6ad-2060a91414c3" />


<img width="1047" height="812" alt="image" src="https://github.com/user-attachments/assets/e13a753f-a706-4464-a621-302817bc212f" />

<img width="1670" height="914" alt="image" src="https://github.com/user-attachments/assets/fe7b2228-556a-4018-a630-a6a37abca468" />

Now we will do the same for OPT2
<img width="1030" height="799" alt="image" src="https://github.com/user-attachments/assets/b30f14ca-5578-4e84-aa1e-447bb65cfcc0" />

<img width="1034" height="794" alt="image" src="https://github.com/user-attachments/assets/7a5f0711-8ebb-4262-89af-116ee39a657c" />

now you do the samething for the other interfaces as well 
for them to have access to internet you will have an open rule going anywhere on the internet 
this is only for configuration purposes and will be secured after everything can talk to each other.


<img width="1038" height="810" alt="image" src="https://github.com/user-attachments/assets/8cd09543-ccf8-4be1-ac0f-41beb04d5e11" />

<img width="1026" height="798" alt="image" src="https://github.com/user-attachments/assets/e6eaa27f-4e7a-43e7-a710-e88234bc45cf" />

and you should have this finally

<img width="739" height="444" alt="image" src="https://github.com/user-attachments/assets/d8d9ff3a-198e-4467-af7c-5248e6828b2b" />

Now we are going to statically assign those IP adress to the domain controler and other devices.

<img width="1688" height="1109" alt="image" src="https://github.com/user-attachments/assets/fe379363-1886-4baf-b1f6-afe8f8596d8d" />




