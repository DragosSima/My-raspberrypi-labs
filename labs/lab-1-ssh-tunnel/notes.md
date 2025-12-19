# Lab 1 – SSH Access from Mobile (Terminus)

## Objective
Access the Raspberry Pi via SSH using a mobile device and the Terminus app.  
This setup allows remote administration without a laptop and is the foundation for future labs.

## Requirements
- Raspberry Pi 5 with Raspberry Pi OS
- SSH enabled on the Raspberry Pi
- Mobile device (Android/iOS)
- Terminus app installed
- Both devices connected to the same network

## Step 1 – Enable SSH on Raspberry Pi
Check if SSH is active:

sudo systemctl status ssh

If disabled:

sudo systemctl enable ssh
sudo systemctl start ssh

## Step 2 – Find Raspberry Pi IP Address
Run on the Pi:

ip a

Example result:
192.168.1.50

## Step 3 – Configure Terminus on Mobile
1. Open the **Terminus** app
2. Tap **New Host**
3. Enter:
   - Hostname: Raspberry Pi IP (e.g., 192.168.1.50)
   - Port: 22
   - Username: pi
4. Save the connection

## Step 4 – Connect via SSH
Tap the saved host in Terminus.

If prompted:
- Accept the SSH fingerprint
- Enter the Raspberry Pi password

You should now see the terminal prompt of the Pi.

## Step 5 – Verify Connection
Run basic commands:

whoami
hostname
uptime
ls -la

## Notes
This lab confirms that mobile SSH access works correctly and will be used in later labs for:
- network configuration
- ACL testing
- segmentation scenarios
- remote administration
