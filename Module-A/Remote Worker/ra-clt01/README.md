#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Remote Worker/ra-clt01/" alt="FW-HQ" width="160" height="160">
  </a>
  <h1 align="center">RA-CLT01</h1>
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