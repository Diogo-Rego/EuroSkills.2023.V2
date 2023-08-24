#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/web_server.png" alt="APACHE2" width="160" height="160">
  </a>
  <h1 align="center">DMZ-HOST</h1>
</p>

## Setup Guide

- [X] General Configuration - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#general-configuration)
  - [X] Set the hostname  - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#set-the-hostname)
  - [X] Network configuration  - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#configure-the-network-interface---ipv4)
  - [X] Set the time zone - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#configure-the-time-zone)
  - [X] Set the keyboard layout - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#configure-the-keyboard-layout)
  - [X] Install SSH server and allow root password access - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-and-configure-the-ssh-server)
- [X] Preinstalled Resources - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#preinstalled-resources)
  - [X] Install the test tools - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-the-test-tools)
- [X] Install DNS server - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-dns-server)
  - [X] Install BIND9 - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-the-bind9)
  - [X] Create a Domain - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-bind9)
  - [X] Create a Zones - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-bind9)
    - [X] Configure forward records - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-bind9)
    - [X] Configure reverse records - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-bind9)
  - [X] Configure the Dynamic DNS - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#configure-the-dynamic-dns---bind9)
    - [X] Create our key for DHCP Update - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-1-create-key-file)
- [X] Install Web server - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-web-server)
  - [X] Install APACHE2 - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-the-apache2)
    - [X] Configure SSL - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#configure-the-ssl---apache2)
    - [ ] Configure Client Certification Authentication - [Click Here]()
- [X] Install Email server - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-email-server)
  - [X] Install Postfix - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#install-the-postfix)
    - [X] Configure SSL - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-postfix)
    - [X] Configure Mail Folder - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-2-configure-postfix)
      - [X] Create Mail Folder for all Users - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-4-configure-mailboxes-and-users)
  - [X] Install Dovecot - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-1-install-the-necessary-software)
    - [X] For imap - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-3-configure-dovecot)
    - [X] For pop3 - [Click Here](https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#step-3-configure-dovecot)

## General Configuration

<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/hostname.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="HOSTNAME" width="160" height="160">
  </a>
  <h1 align="center">Set the hostname</h1>
</p>

### Step 1: To set a new hostname

- Use the ``hostnamectl`` command with superuser privileges

````
sudo hostnamectl set-hostname new-hostname
````

Replace **'new-hostname'** with the desired hostname.

-  After running the command, you might need to restart your system for the changes to take effect:

````
sudo reboot
````

After the reboot, your Debian machine should be using the new hostname. To verify the new ``hostname``, you can use the hostname command:

````
hostname
````

#
<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/wired-network.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="NETWORK INTERFACES - IPV4" width="160" height="160">
  </a>
  <h1 align="center">Configure the Network Interface - IPV4</h1>
</p>

### Step 1: Identify Network Interfaces

- Determine the network interface names using the ip command or by checking the ``/etc/network/interfaces`` file. Common interface names are ``eth0`` for Ethernet and ``wlan0`` for wireless.

### Step 2: Edit Network Configuration File

- Open the network configuration file using a text editor:

````
sudo nano /etc/network/interfaces
````

### Step 3: Configure Network Interfaces

- Modify the file to define the network configuration for each interface. Here's an example configuration for a typical Ethernet interface (``eth0``):

````
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
    address 192.168.1.100   # Replace with your desired IP address
    netmask 255.255.255.0   # Replace with your subnet mask
    gateway 192.168.1.1     # Replace with your gateway IP address
    dns-nameservers 8.8.8.8 8.8.4.4   # Replace with your DNS servers
    dns-search example.com            # Replace with your name DNS servers
````

- If you are using DHCP to obtain IP address configuration automatically, you can use the following configuration instead:

````
auto eth0
iface eth0 inet dhcp
````

- Adjust the configuration based on your network requirements, including IP address, subnet mask, gateway, and DNS servers.

### Step 4: Save the file and exit the text editor.

### Step 5: Restart Networking Service

- Restart the networking service to apply the changes:

````
sudo systemctl restart networking
````

### Step 6: Verify Network Configuration

- Use the ``ip`` command or other network tools (``ifconfig``, ``ping``, etc.) to verify that the network interface is configured correctly and functioning as expected.

#
<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/time-zone.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="TIMEZONE" width="160" height="160">
  </a>
  <h1 align="center">Configure the time zone</h1>
</p>

### Step 1: To view the list of available timezones

- Run the following command:

````
timedatectl list-timezones
````

This command will display a long list of timezones. Scroll through the output to find the desired timezone.

### Step 2: Once you have identified the desired timezone

- Use the following command to set it:

````
sudo timedatectl set-timezone [timezone]
````

Replace ``[timezone]`` with the timezone you want to configure. For example, to set the timezone to "Europe/Warsaw," the command would be:

### Step 3: After running the command

- ``timedatectl`` will update the system's timezone configuration.

### Step 4: To verify the changes

- Run the following command:

````
timedatectl
````

#
<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/keyboard_layouts.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="Keyboard Layout" width="160" height="160">
  </a>
  <h1 align="center">Configure the Keyboard Layout</h1>
</p>

### Step 1: Check the available keyboard layouts by running

````
sudo dpkg-reconfigure keyboard-configuration
````

1. You'll be presented with a configuration dialog that allows you to select your keyboard layout, keyboard model, and other options. Use the arrow keys to navigate and the spacebar to select options.

2. Once you have selected the desired keyboard layout and options, save the changes and exit the configuration dialog.

3. After making the changes, apply the new configuration by running:

````
sudo service keyboard-setup restart
````

OR

````
sudo reboot
````

#
<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/ssh.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="SSH" width="160" height="160">
  </a>
  <h1 align="center">Install and configure the SSH server</h1>
</p>


### Step 1: Install the OpenSSH Server

- Open a terminal on your Debian machine and use the following command to install the OpenSSH server:

````
sudo apt update
sudo apt install openssh-server
````

This will download and install the OpenSSH server on your system.

### Step 2: Configure Root Password Access

- Open the SSH server configuration file in a text editor:

````
sudo nano /etc/ssh/sshd_config
````

- Look for the line that says:

````
#PermitRootLogin prohibit-password
````

- Change it to:

````
PermitRootLogin yes
````

- Save the file and exit the text editor.

### Step 3: Restart the SSH Server:

After making the changes to the SSH configuration, you need to restart the SSH server for the changes to take effect:

````
sudo systemctl restart sshd
````

OR

````
sudo service sshd restart
````

## Preinstalled Resources

<p align="center">
  <a>
    <img src="../../../img/Module-A/general_configuration/install.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="Keyboard Layout" width="160" height="160">
  </a>
  <h1 align="center">Install the test tools</h1>
</p>

### Step 1: For testing purpose

- All VM has been installed with the following test tools:

````
sudo apt install -y smbclient curl lynx dnsutils ldap-utils ftp lftp wget ssh nfs-common rsync telnet traceroute tcptraceroute tcpdump net-tools cifs-utils
````

## Install DNS server

#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/bind9.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="BIND9" width="160" height="160">
  </a>
  <h1 align="center">Install the BIND9</h1>
</p>

### Step 1: Install Bind9

```
sudo apt update
sudo apt install bind9 resolvconf
```

### Step 2: Configure Bind9

**2.1. Edit the main Bind9 configuration file:**

```
sudo nano /etc/bind/named.conf.options
```

* Add or modify the following lines in the options section:

```
options {
    directory "/var/cache/bind";
    forwarders {
        8.8.8.8;
        8.8.4.4;
    };
    dnssec-validation no;
    allow-recursion { any; };
    auth-nxdomain no;    # Disable DNSSEC error showing as SERVFAIL
    listen-on-v6 { any; };
};
```

In this example, we set Google DNS servers ``(8.8.8.8 and 8.8.4.4)`` as forwarders. Adjust them according to your preference.

**2.2. Create a new zone configuration file:**

```
sudo nano /etc/bind/named.conf.local
```

* Add the following lines to define your DNS zone:

```
zone "localhost" {
    type master;
    file "/var/cache/bind/db.localhost.com";
    allow-update { none; };
};

zone "x.x.x.in-addr.arpa" {
    type master;
    file "/var/cache/bind/db.x.x.x";
    allow-update { none; };
};
```

Replace ``localhost`` with your domain name and ``x.x.x`` with the reverse DNS zone corresponding to your IP address range.

**2.3. Create the forward zone file:**

```
sudo nano /var/cache/bind/db.localhost
```

* Add the following content and modify it according to your needs:

```
$TTL    604800
@       IN      SOA     localhost. root.localhost. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      localhost.
@       IN      A       127.0.0.1
@       IN      AAAA    ::1
```

Replace ``localhost`` with your domain name and ``127.0.0.1`` with the IP address of your DNS server.

**2.4. Create the reverse zone file:**

```
sudo nano /var/cache/bind/db.x.x.x
```

* Add the following content and modify it according to your needs:

```
$TTL    604800
@       IN      SOA     localhost. root.localhost. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      localhost.
1.0   IN      PTR     localhost.
```

Replace ``localhost`` with your domain name and ``1.0`` with the last octet of your server's IP address.

### Step 3: Restart Bind9

```
sudo systemctl restart bind9
```

### Step 4: Test the configuration

* You can check the status of Bind9 using the following command:

```
sudo systemctl status bind9
```

* Additionally, you can test the DNS resolution by running the following command:

```
nslookup example.com
```

OR

```
dig example.com @127.0.0.1
```

#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/ddns_bind9.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="Dynamic DNS" width="160" height="160">
  </a>
  <h1 align="center">Configure the Dynamic DNS - BIND9</h1>
</p>

### Step 1: Create Key File

- Create a key file to keep the password separate from the main file
- On the DNS server, switch to the bind folder

```
cd /etc/bind
```

- Then create our key by running the following command

```
ddns-confgen -k <Key-Name>
```

- Copy the key example and modify to suit, e.g.

```
key "DHCP_UPDATER" {  
	algorithm hmac-sha256;  
	secret "/mAXOLTQUp8V9XzYnw88dkOkiDXBU6SNv/jEL3IgKVE=";  
}; 
```

### Step 2: Update DNS Configuration

The DNS server configuration needs to be updated as the zone files have been moved
It needs to know where to find the key, where to find the zone files we’ve moved and be configured to allow updates from the DHCP server

- First, make a backup copy of the file

```
sudo cp named.conf.local named.conf.local.old
sudo nano named.conf.local
```

- And then apply our changes

**``sudo nano named.conf.local``**

```
key "DHCP_UPDATER" {  
	algorithm hmac-sha256;  
	secret "/mAXOLTQUp8V9XzYnw88dkOkiDXBU6SNv/jEL3IgKVE=";  
}; 

zone "localhost" {
    type master;
    file "/var/cache/bind/db.localhost.com";
    allow-update { DHCP_UPDATER; };
};

zone "x.x.x.in-addr.arpa" {
    type master;
    file "/var/cache/bind/db.x.x.x";
    allow-update { DHCP_UPDATER; };
};
```

**``sudo nano named.conf.option``**

```
options {
        forwarders{
                8.8.8.8;
        };
        dnssec-validation no;
        auth-nxdomain no; 
        allow-recursion { any; };
        listen-on-v6 { any; };
}
```

- Check the DNS server configuration syntax

```
sudo named-checkconf
```

- Then restart and check the bind9 status

```
sudo systemctl restart bind9
sudo systemctl status bind9
```

## Install Web server

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/apache2.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="APACHE2" width="260" height="160">
  </a>
  <h1 align="center">Install the APACHE2</h1>
</p>

### Step 1: Install Apache2

```
sudo apt install apache2
```

### Step 2: Locate the Apache2 Document Root

- Apache2 serves files from a directory known as the Document Root.
- By default, the Document Root is ``/var/www/html`` on Ubuntu and Debian. You can place your web page files in this directory or modify the Document Root as per your requirements.

### Step 3: Create your web page

- Use a text editor to create your web page file. For example, you can use nano to create a new HTML file named ``index.html``:

```
sudo nano /var/www/html/index.html
```

- Inside the file, add your HTML content. Here's a simple example:

```
<!DOCTYPE html>
<html>
<head>
    <title>My Web Page</title>
</head>
<body>
    <h1>Welcome to My Web Page</h1>
    <p>This is a sample web page.</p>
</body>
</html>
```

### Step 4: Save the file and exit the text editor.

### Step 5: Set appropriate file permissions

- Ensure that the file has appropriate read permissions so that Apache2 can serve it. In most cases, the default permissions are sufficient. You can use the following command to ensure the file has the correct permissions:

```
sudo chmod 644 /var/www/html/index.html
```

### Step 6: Start/restart Apache2

- If Apache2 is not already running, start it using the appropriate command for your operating system. For example, on Ubuntu or Debian, you can use:

```
sudo service apache2 start
```

- If Apache2 is already running, you can restart it with:

```
sudo service apache2 restart
```

### Step 7: Access your web page

- Open a web browser and enter your server's IP address or domain name in the address bar. You should see your web page displayed.

#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/ssl.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="APACHE2 + SSL" width="160" height="160">
  </a>
  <h1 align="center">Configure the SSL - APACHE2</h1>
</p>

### Step 1: Obtain SSL/TLS Certificates

- Before adding certificates to Apache2, you need to obtain SSL/TLS certificates. You can obtain them from a trusted certificate authority (CA) or use a self-signed certificate for testing purposes. Here are the general steps for obtaining certificates:

    * Generate a private key: Use a tool like OpenSSL to generate a private key file (e.g., ``private.key``). Keep this key file secure.

    * Create a certificate signing request (CSR): Use the private key to generate a CSR file (e.g., ``certificate.csr``). The CSR contains information about your server and is used to request a certificate from a CA.

    * Submit the CSR to a CA: Submit the CSR to a trusted CA and follow their instructions to obtain the SSL/TLS certificate. The CA will typically provide you with a certificate file (e.g., ``certificate.crt``).

### Step 2: Enable SSL/TLS Module

- Apache2 needs the SSL/TLS module enabled to support HTTPS. Run the following command to enable the module:

```
sudo a2enmod ssl
```

### Step 3: Create a Certificate File

- Combine your SSL/TLS certificate (``certificate.crt``) and the CA's intermediate certificate(s) into a single file. You can use a text editor to concatenate the files. Save the combined file as ``yourdomain.crt``. For example:

```
cat certificate.crt intermediate.crt > yourdomain.crt
```

- If you have a bundle of intermediate certificates, make sure to include them in the concatenation.

### Step 4: Configure Apache2 to Use SSL/TLS

- Edit the virtual host configuration file for your domain (e.g., ``mydomain.conf``) that you created earlier. Add the following SSL/TLS-related directives inside the ``<VirtualHost>`` block:

```
<VirtualHost *:443>
    ServerName yourdomain.com
    ServerAlias www.yourdomain.com
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /path/to/yourdomain.crt
    SSLCertificateKeyFile /path/to/private.key
    # Optional: SSLCertificateChainFile /path/to/intermediate.crt

    <Directory /var/www/html>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Make sure to replace ``/path/to/`` with the actual paths to your certificate and private key files.

**Note:** If you have a separate intermediate certificate file, you can uncomment the ``SSLCertificateChainFile`` directive and provide the path to the intermediate certificate file.

### Step 5: Save the virtual host configuration file and exit the text editor.

### Step 6: Enable the SSL/TLS virtual host

- Run the following command to enable the SSL/TLS virtual host configuration:

```
sudo a2ensite mydomain.conf
```

### Step 7: Restart Apache2

- Restart Apache2 to apply the changes:

```
sudo service apache2 restart
```

### Step 8: Test HTTPS

- Open a web browser and enter your domain name with ``https://`` (e.g., ``https://yourdomain.com``). If the configuration is correct, you should see your website served over HTTPS.


## Install Email server

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/dmz-host/postfix.png" href="https://github.com/Diogo-Rego/EuroSkills.2023.V2/tree/main/Module-A/Corporate%20HQ/dmz-host#dmz-host" alt="APACHE2 + SSL" width="250" height="160">
  </a>
  <h1 align="center">Install the Postfix</h1>
</p>

### Step 1: Install the necessary software

- Install the Postfix mail server:

```
sudo apt install postfix
```

- During the installation process, select "Internet Site" as the configuration type, and enter your domain name when prompted.

- Install other required packages, such as Dovecot for handling incoming email and authentication:

```
sudo apt install dovecot-imapd dovecot-pop3d
```

### Step 2: Configure Postfix

- Edit the Postfix main configuration file:

```
sudo nano /etc/postfix/main.cf
```

- Configure the following settings:

```
# TLS parameters
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_tls_security_level=may

smtp_tls_CApath=/etc/ssl/certs
smtp_tls_security_level=may

myhostname = yourdomain.com
mydestination = $myhostname, localhost, localhost.localdomain

mynetworks = 0.0.0.0/0

home_mailbox = Maildir/
```

- Save the file and exit the text editor.

### Step 3: Configure Dovecot

- Edit the Dovecot configuration file:

```
sudo nano /etc/dovecot/dovecot.conf
```

- Add or modify the following lines:

```
# Add the protocols you wish to enable.
protocols = imap pop3
```

- Edit the ssl configuration file:

````
nano /etc/dovecot/conf.d/10-ssl.conf
````

- Add or modify the following lines:

```
ssl_cert = </etc/dovecot/private/dovecot.pem
ssl_key = </etc/dovecot/private/dovecot.key

ssl_client_ca_dir = /etc/ssl/certs
```

- Edit the mailbox configuration file:

````
nano /etc/dovecot/conf.d/10-mail.conf
````

- Uncomment or modify the following lines:

```
   mail_location = maildir:~/Maildir
   
#mail_location = mbox:~/mail:INBOX=/var/mail/%u
```

- Save the file and exit the text editor.

### Step 4: Configure mailboxes and users

- Create a mailbox directory for each user in ``/etc/skel``:

````
maildirmake.dovecot Maildir/
````

- Create a system user for each mailbox:

```
sudo adduser
```

### Step 5: Configure email clients

- To access emails using IMAP or POP3, configure your email clients (e.g., Outlook, Thunderbird) with the appropriate settings:

    * Incoming mail server (IMAP): yourdomain.com, port 143 (STARTTLS)

    * Incoming mail server (POP3): yourdomain.com, port 110 (STARTTLS)

    * Outgoing mail server (SMTP): yourdomain.com, port 25 (STARTTLS)

### Step 6: Restart services

- Restart Postfix and Dovecot to apply the configuration changes:

```
sudo systemctl restart postfix
sudo systemctl restart dovecot
```

That's a basic outline of setting up an email server in Debian using Postfix and Dovecot. Configuring and securing an email server requires additional considerations, such as setting up spam filters, enabling SSL/TLS, configuring DNS records, and implementing security best practices. It's recommended to consult detailed documentation or seek professional assistance when setting up an email server for production use.
