#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/fw-hq/iptables-firewall.png" alt="FW-HQ" width="160" height="160">
  </a>
  <h1 align="center">FW-HQ</h1>
</p>

## Setup Guide

- [X] General Configuration - [Click Here]()
  - [X] Set the hostname  - [Click Here]()
  - [X] Network configuration  - [Click Here]()
  - [X] Set the time zone - [Click Here]()
  - [X] Set the keyboard layout - [Click Here]()
  - [X] Install SSH server and allow root password access - [Click Here]()
- [X] Preinstalled Resources - [Click Here]()
  - [X] Install the test tools - [Click Here]()
- [X] Install Certification Authority - [Click Here]()
  - [X] Install Easy-RSA - [Click Here]()
    - [X] Create a root certificate authority - [Click Here]()
- [X] Install Iptables - [Click Here]()
  - [X] Configure NAT - [Click Here]()
    - [X] Enable IP forwarding - [Click Here]()
    - [X] Configure iptables port forwarding rule - [Click Here]()
      - [X] Enable IP masquerading - [Click Here]()
  - [ ] Configure Firewall - [Click Here]()
    - [ ] Configure firewall with iptables - [Click Here]()
      - [ ] Incoming packets should be dropped by default - [Click Here]()
      - [ ] Allow minimal traffic for the services to work - [Click Here]()
      - [ ] Make sure, that iptables persist across reboots - [Click Here]()
- [ ] Install DHCP Relay - [Click Here]()
  - [ ] Install isc-dhcp-relay - [Click Here]()
    - [ ] Configure DHCP Relay - [Click Here]()
- [ ] Install VPN server - [Click Here]()
  - [ ] Install OpenVPN - [Click Here]()
    - [ ] Create secure channel - [Click Here]()
      - [ ] Configure the Site-to-Site VPN (Server) - [Click Here]()
      - [ ] Configure the Remote Access VPN - [Click Here]()

## General Configuration

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/general_configuration/hostname.png" alt="HOSTNAME" width="160" height="160">
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
  <a href="">
    <img src="../../../img/Module-A/general_configuration/wired-network.png" alt="NETWORK INTERFACES - IPV4" width="160" height="160">
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
  <a href="">
    <img src="../../../img/Module-A/general_configuration/time-zone.png" alt="TIMEZONE" width="160" height="160">
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
  <a href="">
    <img src="../../../img/Module-A/general_configuration/keyboard_layouts.png" alt="Keyboard Layout" width="160" height="160">
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
  <a href="">
    <img src="../../../img/Module-A/general_configuration/ssh.png" alt="SSH" width="160" height="160">
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
  <a href="">
    <img src="../../../img/Module-A/general_configuration/install.png" alt="Keyboard Layout" width="160" height="160">
  </a>
  <h1 align="center">Install the test tools</h1>
</p>

### Step 1: For testing purpose

- All VM has been installed with the following test tools:

````
sudo apt install -y smbclient curl lynx dnsutils ldap-utils ftp lftp wget ssh nfs-common rsync telnet traceroute tcptraceroute tcpdump net-tools cifs-utils
````

## Install Certification Authority

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/fw-hq/" alt="Install Easy-RSA" width="160" height="160">
  </a>
  <h1 align="center">Install Easy-RSA</h1>
</p>

### To view the manual pages for Easy-RSA, you can use the ``./easyrsa`` command followed by the ``help`` command you want to learn more about

- Here are some examples:

  - To view the manual page for the ``easyrsa`` command itself:

```
./easyrsa help
```

  - To view the manual page for a specific Easy-RSA command, such as ``alt-name``:

```
./easyrsa help altname
```

### Step 1: Install EasyRSA on your Debian system if you haven't already

- You can typically do this by installing the ``easy-rsa`` package:

```
sudo apt-get install easy-rsa
```

### Step 2: Once installed 

- Copy the EasyRSA directory for other directory:

```
cp -R /usr/share/easy-rsa/ /etc/
```

### Step 3: Navigate to the EasyRSA directory

```
cd /etc/easy-rsa/
```

### Step 4: Copy the ``vars.example`` file to a new file (let's call it ``vars``)

```
cp vars.example vars
```

### Step 5: Open the ``vars`` file using a text editor

```
nano vars
```

### Step 6: Modify the variables in the ``vars`` file according to your requirements

- For example, you may need to set the following variables:

```
set_var EASYRSA_DN      "org"

set_var EASYRSA_REQ_COUNTRY     ""
set_var EASYRSA_REQ_PROVINCE    ""
set_var EASYRSA_REQ_CITY        ""
set_var EASYRSA_REQ_ORG         ""
set_var EASYRSA_REQ_EMAIL       ""
set_var EASYRSA_REQ_OU          ""

set_var EASYRSA_REQ_CN          ""

set_var EASYRSA_BATCH          "yes"
```

- Adjust the values to match your desired organization details.

### Step 7: Save and exit the ``vars`` file

### Step 8: Initialize the EasyRSA environment and build the Certificate Authority (CA)

```
./easyrsa init-pki
./easyrsa build-ca
```

- This command will generate a server certificate signing request (CSR) without a passphrase.

### Step 9: Sign the certificate using the CA

- For Server:

```
./easyrsa build-server-full srv.name nopass
```

- For Client:

```
./easyrsa build-clint-full cli.name nopass
```

### Step 10: Sign a certificate signing request (CSR) with the Common Name (CN) ``"www.test.pt"`` and an additional Subject Alternative Name (SAN)

```
./easyrsa --subject-alt-name="DNS:www.test.pt" sign-req server www.test.pt
```

## Install Iptables

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/fw-hq/" alt="Configure NAT" width="160" height="160">
  </a>
  <h1 align="center">Configure NAT</h1>
</p>

### Step 1: Install iptables (if not already installed)

Most Debian installations come with iptables pre-installed. If it's not present on your system, install it using the following command:

````
sudo apt update
sudo apt install iptables
````

To make the iptables rules persistent across reboots, you can use the iptables-persistent package, which is available in Debian:

````
sudo apt install iptables-persistent
````

During the installation, it will ask you whether you want to save the current IPv4 rules. Select "Yes" to save them.

### Step 2: Enable IP forwarding

IP forwarding must be enabled for your system to act as a router and perform NAT.

- Open the sysctl.conf file to make this change:

````
sudo nano /etc/sysctl.conf
````

- Uncomment or add the following line to enable IP forwarding:

````
net.ipv4.ip_forward=1
````

- Save the file and apply the changes with:

````
sudo sysctl -p
````

### Step 3: Configure iptables port forwarding rule

Open a terminal and run the following iptables command to set up the port forwarding rule:

````
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 192.168.1.100:80
````

In this command:

- ``-t nat``: Specifies the NAT table in iptables.

- ``-A PREROUTING``: Appends the rule to the PREROUTING chain, which is used for altering incoming packets.

- ``-i eth0``: Specifies the network interface through which the incoming traffic arrives (replace eth0 with your actual internet-facing interface).

- ``-p tcp``: Specifies that the forwarding is for TCP traffic.

- ``--dport 80``: Specifies the destination port (port 80 for HTTP).

- ``-j DNAT``: Redirects the packet to the specified destination address.

- ``--to 192.168.1.100:80``: Specifies the local IP address (192.168.1.100) and port (80) to which the traffic will be forwarded.

### Step 4: Enable IP masquerading (if not already enabled)

IP masquerading allows the response traffic from the local server to go back through the Debian machine, which acts as a gateway.

````
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
````

Replace ``eth0`` with your actual internet-facing interface.

### Step 5: Save iptables rules

To save the current iptables rules to be loaded on boot, use the following commands:

````
netfilter-persistent save
````

### Step 5: Reload iptables rules

````
netfilter-persistent reload
````

- IPv4 Rules: The rules for IPv4 are saved in the /etc/iptables/rules.v4 file.
- IPv6 Rules: The rules for IPv6 are saved in the /etc/iptables/rules.v6 file.

The package iptables-persistent automatically loads the rules from these two files during system startup, applying the saved rules to configure the iptables firewall.


## Configure Firewall

## Install VPN server

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/fw-hq/" alt="Install the OpenVPN" width="160" height="160">
  </a>
  <h1 align="center">Install the OpenVPN</h1>
</p>

### Step 1: Install OpenVPN

- Update your package repository:

```
sudo apt update
```

- Install OpenVPN:

```
sudo apt install openvpn
```

### Step 2: Create OpenVPN Server Configuration

Now that both your client and server certificates and keys have been generated, you can begin configuring the OpenVPN service to use these credentials.

- Start by copying a sample OpenVPN configuration file into the configuration directory to use as a basis for your setup:

```
sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/
```

- Open the server configuration file in your preferred text editor:

```
sudo nano /etc/openvpn/server.conf
```

- Add or modify the following content to the file (adjust parameters as needed):

```
port 1194
proto udp

dev-type tun
dev tun-remote # Name for Tunnel

ca /etc/openvpn/easy-rsa/pki/ca.crt
cert /etc/openvpn/easy-rsa/pki/issued/server.crt
key /etc/openvpn/easy-rsa/pki/private/server.key

# Diffie hellman parameters.
# Generate your own with:
#   openssl dhparam -out dh2048.pem 2048
dh /etc/openvpn/easy-rsa/pki/dh.pem

# Configure server mode and supply a VPN subnet
# for OpenVPN to draw client addresses from.
server 10.8.0.0 255.255.255.0

ifconfig-pool-persist ipp.txt

# Push routes to the client to allow it
# to reach other private subnets behind
# the server.
push "dhcp-option DNS 8.8.8.8"

# If enabled, this directive will configure
# all clients to redirect their default
# network gateway through the VPN, causing
# all IP traffic such as web browsing and
# and DNS lookups to go through the VPN
push "redirect-gateway def1 bypass-dhcp"

keepalive 10 120

# For extra security beyond that provided
# by SSL/TLS, create an "HMAC firewall"
# to help block DoS attacks and UDP port flooding.
#
# Generate with:
#   openvpn --genkey tls-auth ta.key
tls-auth /etc/openvpn/easy-rsa/pki/ta.key 0

key-direction 0
cipher AES-256-CBC
auth SHA256
comp-lzo
user nobody
group nogroup
persist-key
persist-tun
status openvpn-status.log
verb 3
explicit-exit-notify 1
```

Save and exit the file (CTRL+O to save, CTRL+X to exit).


### Step 3: Enable IP Forwarding

- Enable IP forwarding:

```
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### Step 4: Configure Firewall

- Allow OpenVPN traffic through the firewall:

```
sudo iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -s 10.8.0.0/24 -j ACCEPT
sudo iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE
```

**Note:** Replace ``eth0`` with the appropriate network interface.

- Save the firewall rules:

```
sudo iptables-save | sudo tee /etc/iptables/rules.v4
```

### Step 5: Start OpenVPN and Enable Autostart

- Start OpenVPN and enable it to start on boot:

```
openvpn --config /etc/openvpn/server/server.conf  # Test configuration
systemctl enable openvpn-server@server
systemctl start openvpn-server@server
systemctl status openvpn-server@server
```

### Step 6: Generate Client Certificates

- Generate client certificates using the EasyRSA scripts, similar to the server keypair generation.

### Step 7: Distribute Client Configurations

- Copy the following files to your client devices:

  - ``client.crt``
  - ``client.key``
  - ``ca.crt``
  - ``ta.key``
  - ``client.ovpn`` (Create this file with client-specific configuration.)

- Create a ``client.ovpn`` file for each client device with the following content:

```
client
dev tun
proto udp
remote SERVER_IP 1194
resolv-retry infinite
nobind
persist-key
persist-tun
remote-cert-tls server
auth SHA256
cipher AES-256-CBC
comp-lzo
key-direction 1
verb 3
<ca>
(Insert content of ca.crt here)
</ca>
<cert>
(Insert content of client.crt here)
</cert>
<key>
(Insert content of client.key here)
</key>
<tls-auth>
(Insert content of ta.key here)
</tls-auth>
```

- Replace ``SERVER_IP`` with your server's IP address.

### Step 8: Connect Clients

- Install OpenVPN client software on client devices.

- Import or paste the contents of the ``client.ovpn`` configuration into the client software.

- Connect to the OpenVPN server.
