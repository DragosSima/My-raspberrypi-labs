Lab 2 – SSH Authentication with Public Key

Objective
Configure passwordless SSH authentication from both PC and mobile using public key authentication.
This improves security, removes password prompts, and prepares the environment for future labs.

Requirements
• 	Raspberry Pi 5 with Raspberry Pi OS
• 	SSH enabled on the Raspberry Pi
• 	PC with SSH client
• 	Mobile device with Terminus installed
• 	Both devices on the same network

Step 1 – Generate SSH Key on PC
On the PC, generate an ED25519 SSH key:
ssh-keygen -t ed25519
Press Enter to accept the default path.
The public key will be located at:
~/.ssh/id_ed25519.pub

Step 2 – Generate SSH Key on Mobile (Terminus)
In the Terminus app:
1. 	Go to Settings → Keys
2. 	Create a new ED25519 key
3. 	Copy the public key
Now you have two public keys: one from the PC and one from the mobile device.

Step 3 – Add Public Keys to Raspberry Pi
Connect to the Raspberry Pi using your password (only this time), then edit the authorized_keys file:
nano ~/.ssh/authorized_keys
Paste both public keys, one per line. Example:
ssh-ed25519 AAAA... phone
ssh-ed25519 AAAA... pc
This file defines which devices are allowed to authenticate without a password.

Step 4 – Test SSH Authentication
From the PC:
ssh pi@<raspberry-ip>
From the mobile (Terminus):
• 	Tap the saved host
• 	It should connect without asking for a password
If both devices connect successfully, the configuration is correct.

Screenshot
Example of a correctly configured authorized_keys file:
Authorized keys example
![Authorized keys example](../../docs/images/ssh_public_keys.png)

Notes
This lab confirms that passwordless SSH access works correctly and will be used in later labs for:
• 	multi-device administration
• 	Docker network configuration
• 	ACL and segmentation testing
• 	secure remote access


