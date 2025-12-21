Lab 2 — SSH Authentication with Public Key
This lab explains how to configure secure, passwordless SSH authentication from both a PC and a mobile device to a Raspberry Pi. It builds on the previous lab and focuses on generating SSH keys, deploying them, and validating access.

✅ Objective
• 	Generate SSH key pairs on each client device
• 	Deploy public keys to the Raspberry Pi
• 	Configure the authorized_keys file
• 	Test passwordless SSH authentication

✅ 1. Generate SSH Key on PC
On your PC, generate an ED25519 SSH key:
ssh-keygen -t ed25519
Press Enter to accept the default path and leave the passphrase empty (optional).
The public key will be stored in:
~/.ssh/id_ed25519.pub

✅ 2. Generate SSH Key on Mobile (Termius)
In Termius:
1. 	Go to Settings → Keys
2. 	Create a new ED25519 key
3. 	Copy the public key

✅ 3. Add Public Keys to the Raspberry Pi
Connect to the Raspberry Pi and open the authorized_keys file:
nano ~/.ssh/authorized_keys
Paste the public keys from both devices (PC and mobile), one per line.
Example:
ssh-ed25519 AAAA... Dragos-phone
ssh-ed25519 AAAA... Dragos-PC
This file defines which devices are allowed to authenticate without a password.

✅ 4. Test SSH Authentication
From your PC:
ssh pi@<raspberry-ip>
From your mobile (Termius):
• 	Tap the host entry
• 	It should connect without asking for a password
If both connections work, the configuration is correct.

✅ Screenshot
Below is an example of a correctly configured authorized_keys file:
Authorized keys example

✅ Conclusion
You now have secure, passwordless SSH access from multiple devices.
This setup improves security, convenience, and prepares the environment for future labs.
