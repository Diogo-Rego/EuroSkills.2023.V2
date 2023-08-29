#
<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/hq-noc/samba-server.png" alt="FW-HQ" width="160" height="160">
  </a>
  <h1 align="center">HQ-NOC</h1>
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
- [X] Configure software-based RAID 5 or RAID 10 - [Click Here]()
  - [X] Install mdadm - [Click Here]()
    - [X] Create the RAID - [Click Here]()
    - [X] Create a filesystem on the array - [Click Here]()
- [ ] Deploy a profile directory of the corporate users - [Click Here]()
  - [ ] Install SAMBA - [Click Here]()
    - [ ] Configure CIFS service - [Click Here]()
        - [ ] Create user profiles on the file system - [Click Here]()
- [X] Create a failover DHCP cluster - [Click Here]()
  - [X] Install DHCP Server - [Click Here]()
    - [X] Configure Secondary DHCP Server - [Click Here]()
    - [X] Add the zones for the Dynameic DNS - [Click Here]()
- [ ] Create monitoring service with Cacti - [Click Here]()
  - [ ] Install Cacti - [Click Here]()
    - [ ] Configure syslog server - [Click Here]()
      - [ ] related to DHCP should be written to ... - [Click Here]()
      - [ ] related to e-mail should be written to ... - [Click Here]()
      - [ ] other incoming logs should be written to ... - [Click Here]()

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

## Configure software-based RAID

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/hq-noc/dhcp.png" alt="Software-based RAID" width="160" height="160">
  </a>
  <h1 align="center">Software-based RAID</h1>
</p>

### Step 1: Installing 'mdadm' and Verify Drives

```
sudo apt install mdadm
```

After the ``mdadm`` package installation, let’s list the four 2GB disks which we have added to our system using ``fdisk`` command.

```
fdisk -l | grep sd
```

Now it’s time to examine the attached four drives for any existing RAID blocks on these drives using the following command.

```
mdadm --examine /dev/sdb /dev/sdc /dev/sdd /dev/sde
```

### Step 2: Partitioning the Disks for RAID

First and foremost, we have to partition the disks (/dev/sdb, /dev/sdc, /dev/sdd and /dev/sde) before adding to a RAID, So let us define the partition using the ``fdisk`` command, before forwarding it to the next steps.

````
fdisk /dev/sdb
fdisk /dev/sdc
fdisk /dev/sdd
fdisk /dev/sde
````

Please follow the below instructions to create a partition on the ``/dev/sdb`` drive.

- Press ``n`` for creating a new partition.

- Then choose ``P`` for the Primary partition. Here we are choosing Primary because there are no partitions defined yet.

- Then choose ``1`` to be the first partition. By default, it will be 1.

- Here for cylinder size, we don’t have to choose the specified size because we need the whole partition for RAID so just Press Enter two times to choose the default full size.

- Next press ``p`` to print the created partition.

- Use ``w`` to write the changes.

Create /dev/sdb Partition

After creating partitions, check for changes in all four drives sdb, sdc, & sdd.

````
mdadm --examine /dev/sdb /dev/sdc /dev/sdd /dev/sde
````

### Step 3: Creating md device ``md0``

````
mdadm --create /dev/md0 --level=10 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
````

- The ``–create`` option tells mdadm to create a new array.

- The ``–level`` specifies the RAID level to be created.

- The ``–raid-devices`` specifies the number of devices, in our case, it’s two devices i.e /dev/sdb1 and /dev/sdc1

After creating raid device, check and verify the RAID, devices included, and RAID Level from the ``mdstat`` output.

````
cat /proc/mdstat
````
OR
````
watch -n1 cat /proc/mdstat
````

After the creation of the raid, Verify the raid devices using the following command.

````
mdadm -E /dev/sd[b-e]1
````

Next, verify the RAID array to assume that the devices which we’ve included in the RAID level are running and started to re-sync.

````
mdadm --detail /dev/md0
````

### Step 4: Creating file system for ``md0``

````
sudo mkfs.ext4 /dev/md0
````

Now create a directory under ``/mnt`` then mount the created filesystem under ``/mnt/raid5`` and check the files under mount point, you will see the lost+found directory.

````
mkdir /mnt/raid5
mount /dev/md0 /mnt/raid5/
ls -l /mnt/raid5/
````

### Step 5: Save Raid 10 Configuration

````
mdadm --detail --scan --verbose >> /etc/mdadm.conf
````

## Create a failover DHCP cluster

<p align="center">
  <a href="">
    <img src="../../../img/Module-A/Corporate HQ/hq-noc/dhcp.png" alt="Failover DHCP cluster" width="160" height="160">
  </a>
  <h1 align="center">Failover DHCP cluster</h1>
</p>

### Step 1: Install the DHCP Server

```
sudo apt update
sudo apt install isc-dhcp-server
```

### Step 2: Configure the DHCP Server

- Open the DHCP server configuration file using a text editor:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Modify the configuration file according to your network settings. Here's an example configuration:

```
# Set the domain name
option domain-name "yourdomain.com";
# Set the DNS servers
option domain-name-servers 8.8.8.8, 8.8.4.4;

# Set the default lease time
default-lease-time 600;
# Set the maximum lease time
max-lease-time 7200;

# Configure the DHCP subnet
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;  # Define the IP range for dynamic assignment
    option routers 192.168.1.1;  # Set the default gateway
}
```

- Customize the configuration according to your network requirements, including the domain name, DNS servers, lease times, subnet, IP range, and gateway.

- Save the file and exit the text editor.

### Step 3: Configure Primary DHCP Server

After generating a key copy and paste the key on ``dhchp.conf`` and ``named.conf.local``.

- Example of the key generated:

```
key "ddns-key" {
  algorithm hmac-sha256;
  secret "zDQMycm2qO5ERDdGvhMWtjAWAPd6ZxCG0LE1YOsESW+ZRj9pjR+n2hZ/bqYe2dGh8XdQ+TrMKcKfb18JGOHD2g==";
}
```

- Edit the DHCP server configuration file on the primary node:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Add the following to the dhcpd.conf to allow failover with dynamic dns:

```
omapi-port 7911;
omapi-key ddns-key;
```

- Change from auto to standard to auto update dns:

```
ddns-update-style standard;
```

- If you have a static dhcp host configurd add the following to allow the server to give the static ip configute below:

```
update-static-leases on;
```

- Configure the DHCP server options and define the DHCP subnet as per your network requirements.

- Add the following lines at the end of the configuration file to enable failover:

```
failover peer "dhcp-failover" {
    secondary;  # Set as secondary on this node
    address <Secondary-IP>;  # Replace with the IP address of this node
    port 647;  # Use the same port as configured on the primary node
    peer address <Primary-IP>;  # Replace with the IP address of the primary node
    peer port 647;  # Use the same port as configured on the primary node
    max-response-delay 30;  # Maximum delay in seconds for receiving an acknowledgment from the peer
    max-unacked-updates 10;  # Maximum number of unacknowledged updates
    load balance max seconds 3;  # Maximum load balance interval
    mclt 1800;  # Maximum client lead time
}
```

- Then add the zones for the Dynameic DNS:

Key provaided from the ``dhcpd.conf`` documentation for the DDNS:

```
key DHCP_UPDATER {
    algorithm HMAC-MD5.SIG-ALG.REG.INT;
    secret pRP5FapFoJ95JEL06sv4PQ==;
}
```

- Forwarding Zone

```
zone fimatpolska.pl. {
    primary 192.168.10.254;  #DNS server 
    key DHCP_UPDATER;            
}
```

- Reverse Zone

```
zone 0.168.192.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}

zone 15.168.192.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}

zone 0.16.172.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}
```

- Save the file and exit the text editor.

### Step 4: Configure DHCP Reservation

- Open the DHCP server configuration file using a text editor:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Add a DHCP reservation entry for the device at the end of the configuration file. Replace the MAC address (``XX:XX:XX:XX:XX:XX``) and IP address (``192.168.1.10``) with the appropriate values:

```
host mydevice {
    hardware ethernet XX:XX:XX:XX:XX:XX;
    fixed-address 192.168.1.10;
}
```

- Save the file and exit the text editor.

### Step 5: Restart the DHCP Server

```
sudo systemctl restart isc-dhcp-server
```

### Step 6: Verify DHCP Server Operation

```
sudo journalctl -u isc-dhcp-server
```

- Verify that the DHCP server is providing IP addresses to clients by testing on a client device connected to the network.

### Cacti
sudo apt install cacti

sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

sudo nano /etc/php/7.0/apache2/php.ini

sudo mysql -e "SET GLOBAL time_zone = ‘-6:00’;"

sudo dpkg-reconfigure cacti

```
admin
admin
```