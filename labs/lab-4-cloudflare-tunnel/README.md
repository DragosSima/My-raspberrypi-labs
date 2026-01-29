# Lab 4 – Publishing the Company Website Using Cloudflare Tunnel

This lab explains how to publish an internal company website to the internet using Cloudflare, a custom domain, and a Cloudflare Tunnel, without opening any ports on the router. The final public URL for the website is www.simacyber.com

## 1.Domain Registration on Cloudflare

I created a Cloudflare account and added my domain.

Cloudflare provided the nameservers to configure at the domain registrar.

After DNS propagation, Cloudflare became the authoritative DNS manager for the domain.

## 2.Installing Cloudflared on the Raspberry Pi
 
On the Raspberry Pi, I installed cloudflared, the client responsible for creating and maintaining the tunnel.

Updating packages:

sudo apt update && sudo apt upgrade -y

Installing cloudflared (if available in the repository):

sudo apt install cloudflared -y

Alternatively, cloudflared can be installed using the official deb package from Cloudflare.

## 3.Creating the Cloudflare Tunnel

Logging into Cloudflare:

cloudflared tunnel login

This command opens a browser window where I authorized the Raspberry Pi to use my Cloudflare account.

Creating the tunnel:

cloudflared tunnel create company-tunnel

Cloudflare generated a Tunnel ID and a credentials file, for example:

/home/pi/.cloudflared/12345678-abcd-ef01-2345-abcdef123456.json

(The Tunnel ID above is an example and does not represent real credentials.)

## 4.Configuring the Tunnel

I created the configuration file:

sudo nano /etc/cloudflared/config.yml

Configuration content:

tunnel: 12345678-abcd-ef01-2345-abcdef123456

credentials-file: /home/pi/.cloudflared/12345678-abcd-ef01-2345-abcdef123456.json

ingress:

hostname: www.simacyber.com
 
service: http://172.20.0.10:80

service: http_status:404

Where 172.20.0.10 is the internal IP of the container running the company’s Nginx web server.

## 5.Enabling Cloudflared as a System Service
 
Installing the service:

sudo cloudflared service install

Enabling at boot:

sudo systemctl enable cloudflared

Starting the service:

sudo systemctl start cloudflared

Checking the status:

systemctl status cloudflared

If the service is active, the tunnel is running correctly.

## 6.DNS Configuration in Cloudflare
  
Cloudflare automatically created a DNS record for the tunnel:

Type: CNAME

Name: www

Value: something like 12345678-abcd-ef01-2345-abcdef123456.cfargotunnel.com

This record links the domain to the Cloudflare Tunnel without requiring any port forwarding.

## 7.Deploying the Company Website with Nginx
  
Inside the container hosting the company web server, I installed Nginx and deployed a simple HTML page.

Updating packages:

apt update && apt upgrade -y

Installing Nginx:

apt install nginx -y

Checking the service:

systemctl status nginx

Editing the default web page:

nano /var/www/html/index.html

Example content:

SimaCyber – Company Website

Welcome to SimaCyber

This website is served from the internal network through a secure Cloudflare Tunnel.

Public URL: https://www.simacyber.com

## 8.Final Testing
  
Internal Test:

curl http://172.20.0.10

External Test:

https://www.simacyber.com

If the page loads correctly, it confirms that:

the internal Nginx server is reachable

the Cloudflare Tunnel is active

DNS is configured properly

the website is publicly accessible without opening any router ports

