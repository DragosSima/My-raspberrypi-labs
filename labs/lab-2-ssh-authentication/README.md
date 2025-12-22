##Lab 2 – SSH Authentication with Public Key

Objective
Configure passwordless SSH access to the Raspberry Pi from both PC and mobile.
This setup improves security, removes password prompts, and prepares the environment for future labs.

Requirements
• Raspberry Pi 5 with Raspberry Pi OS
• SSH enabled on the Raspberry Pi
• PC with SSH client
• Mobile device (Android/iOS)
• Terminus app installed
• Both devices connected to the same network

Step 1 – Generate SSH Key on PC
Generate an ED25519 SSH key:
ssh-keygen -t ed25519
Press Enter to accept the default path.
The public key will be located at:
~/.ssh/id_ed25519.pub

Step 2 – Generate SSH Key on Mobile (Terminus)
In the Terminus app:
Go to Settings → Keys
Create a new ED25519 key
Copy the public key
Now you have two public keys: one from the PC and one from the mobile device.

Step 3 – Add Public Keys to Raspberry Pi
Connect to the Raspberry Pi using password authentication.
Then open the authorized_keys file:
nano ~/.ssh/authorized_keys
Paste both public keys, one per line. Example:
ssh-ed25519 AAAA… phone
ssh-ed25519 AAAA… pc
This file allows SSH access without a password from trusted devices.

Step 4 – Test SSH Authentication
From the PC:
ssh pi@<raspberry-ip>
From the mobile (Terminus):
Tap the saved host
It should connect without asking for a password
If both connections work, the configuration is correct.

Step 5 – Verify Connection
Run basic commands:
whoami
hostname
uptime
ls -la

Notes
This lab confirms that passwordless SSH access works correctly and will be used in later labs for:
• multi-device administration
• Docker network configuration
• ACL and segmentation testing
• secure remote access
