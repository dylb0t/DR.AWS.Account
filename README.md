# DR.AWS.Account
Steps to spin up an AWS account, eventually will become automated.

# Caveats
For the windows machines, the T2 Micro or T3 Micro for availability zones that do not have T2 are the only ones that fall under the free tier.
These are called burstable instances. I host my VMs out of Sweden because that location does not have T2 Micro. The T3s bursting is a much better system. When you run out of credits it just charges you instead of killing your processor. The T2's processor will drop to pretty terrible when you run out of credits.

Okay, so credits. You may not even use them. For one of my accounts, when he is running his regular script, never bursts because it doesn't run at high CPU. My other account on the other hand does, because my hunting script is a lot more involved. I have also seen that lich can consume a lot of resources but I have not tested this extensively.

So mileage may vary and may take some testing to see where you fall in this.

# Important Note
It will happen at some point that you end up in the wrong region. A reminder, the region selection is in the top right of the screen. Whenever you say "where are my instances?" just look there to make sure you are in the correct region.
<img width="309" height="197" alt="RegionSelection" src="https://github.com/user-attachments/assets/1d55f392-39cb-4353-a6a7-3e7ae355dbe2" />

# Create a Free Account
First, navigate to https://aws.amazon.com and create a free account. There will be questions asking for an email, validation, creditcard and the like. I will not go through those steps on this howto.

# Creation Steps
After selecting the region, you can now create an EC2 instance.
1. Navigate to EC2
The service that you will be using to create your VM is called EC2.
In the top "Search" you can just type EC2.
<img width="974" height="247" alt="1EC2" src="https://github.com/user-attachments/assets/c05a9f50-be3e-4ead-a258-a757e145a44b" />
2. Launch instance
<img width="722" height="197" alt="2LAUNCH" src="https://github.com/user-attachments/assets/e08c6dc3-d6a4-4f0e-b679-f7b018364655" />
3. Give it a name
<img width="874" height="166" alt="3NAME" src="https://github.com/user-attachments/assets/e2351420-a679-4944-a9a9-a9ec642d45bb" />
4. Choose Windows
Make sure you select something that is "free tier eligible". As a note, I use Windows Server 2019 because it is my belief it runs a little faster than 2025. Really this is up to you, as long is it is free.
<img width="889" height="458" alt="4OS" src="https://github.com/user-attachments/assets/2252c7fe-6ba0-462a-82be-23eeae726969" />
5. Choose instance type
Just make sure it says "free tier eligible".  The t2/t3 decision depends on where you choose to host. Sweden is the only place I have found t3 to be free tier eligible at the time of this writing, everything else is t2.
<img width="988" height="244" alt="5SIZE" src="https://github.com/user-attachments/assets/c06ada62-713f-41e2-8550-8c5fa46abab1" />
6. Create keypair
You MUST create a keypair. Download your copy of it as you will need it to connect later.
<img width="1010" height="224" alt="6KEYPAIR" src="https://github.com/user-attachments/assets/f27d3930-4229-4c65-bdad-09dd5f13c832" />
7. Network and Storage
Leave network and storage default for now, as the one selected is free tier eligible. If you choose more storage, you will possibly run into monthly charges. You can lock down your security group to only accept your known IPs if you want, but that is out of the scope of this howto. It would also make it hard to connect from cellphone.
<img width="1013" height="521" alt="7NETWORK" src="https://github.com/user-attachments/assets/023c556c-e41d-4fdc-a74b-98f6e464039c" />
8. Launch
Go take a pee, it will probably be done by the time you get back.
<img width="253" height="144" alt="8LAUNCH" src="https://github.com/user-attachments/assets/8bda2fc6-d739-4a95-a34e-abcdab518bb4" />
9. Navigate to instances
On the left menu you should find Instances.
<img width="254" height="131" alt="9INSTANCES" src="https://github.com/user-attachments/assets/ad02ff41-44bb-4fd7-8b18-45df01006666" />
10. Select instance
<img width="776" height="332" alt="10INSTANCEID" src="https://github.com/user-attachments/assets/f2601d96-e4d2-4b87-8fc2-423f12005ce1" />
11. Connect
Select "Connect" under the actions menu.
<img width="371" height="136" alt="11CONNECT" src="https://github.com/user-attachments/assets/ec2683bf-1da3-4c45-88dd-2a3868415f7f" />
12. Choose RDP Client
<img width="1019" height="673" alt="12RDP" src="https://github.com/user-attachments/assets/33d65af6-b229-448e-b758-5aed49754b60" />
13. Get Password
<img width="881" height="346" alt="13GETPW" src="https://github.com/user-attachments/assets/679fc600-5d4d-4d54-a541-eb5391db30be" />
<img width="388" height="85" alt="16GETPW" src="https://github.com/user-attachments/assets/42763a3c-0934-412e-98f8-c9656f140e2e" />
14. Private Key
Upload the private key that you downloaded when you created the keypair earlier.
<img width="678" height="296" alt="14PK" src="https://github.com/user-attachments/assets/ae275508-757b-4b27-a6cd-e900df68dd4f" />
15. Decrypt
Once you decrypt the password for the Administrator account will show.
<img width="220" height="90" alt="15DECRYPT" src="https://github.com/user-attachments/assets/8c6f60a4-7945-467a-b101-05d2ba05dafa" />
16. Download remote desktop file (optional)
Download the remote desktop file
When prompted use Administrator and your decrypted password
<img width="373" height="131" alt="17DOWNLOADRDP" src="https://github.com/user-attachments/assets/2c56738c-d87c-44ab-9ec9-9b2c2e0205ce" />
17. Done... Or are we?
At this point, you could install genie and run it using the administrator account. However, I prefer to use the administrator account to create a user and add that user to the administrator group. I never log in with the administrator account aside from configuring this user.
I would then log in as the new user and download the appropriate software.
Note that these steps are not included in this howto as genie installation is well documented on the Genie4 repo.
# Pro Tip
Download the software to a folder on your computer, share it to the RDP session. This way, you don't have to configure the browser etc on the server to allow downloads. That is a real PITA. Also, you will have a repository on your computer of everything you will need in 1 year when you have to build this again!
# Pricing Expectations
Even when you use the free tier, you can exceed the amount of credits that are included. In the beginning of this document I talked about 2 accounts that I had. Here is the billing for the first account that doesn't burst often
<img width="1049" height="400" alt="21COSTS" src="https://github.com/user-attachments/assets/31987120-1c21-4459-9548-dc8f96989b78" />
And here is the one that bursts all the time:
<img width="966" height="427" alt="20COSTS" src="https://github.com/user-attachments/assets/0e5040d8-cfd4-43d0-ad77-f2e52bd63073" />
You can track how you are doing by monitoring the CPU credits.
<img width="692" height="242" alt="18CREDITUSAGE" src="https://github.com/user-attachments/assets/44f734e0-f87b-4df2-8255-5777da7f4e29" />
<img width="1571" height="682" alt="19CREDITCOUNT" src="https://github.com/user-attachments/assets/d9956f51-ea61-449b-b46a-3aaa63c5c5b0" />
Credits recover themselves WHILE THE INSTANCE IS ON and NOT BEING USED. So if you use the instance for 8h then log off you will likely sit more like the first image, assuming you aren't doing heavy lifting lol.
You will likely need to build your own baseline for this, just be prepared to have to pay anything from $0.00 to a few bucks depending on what you do.
# Expiry
Just remember, in a year free tier ends and you will be expected to pay for your usage. I have found this has cost me ~20.00 /month. The easiest way to build the new account is to create an AMI image in your current account and share it with the new one. Then spin it up in your new account and it will have all your apps installed and current data already.



