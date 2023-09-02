apt install dpkg-dev
apt install apache2

```
mount /dev/sr0 /media/cdrom0
mount /dev/sr1 /media/cdrom1
mount /dev/sr2 /media/cdrom2
mount /dev/sr3 /media/cdrom3
```

```
cd /var/www/html/sr1/ && ln -s /media/cdrom1 1
cd /var/www/html/sr2/ && ln -s /media/cdrom2 2
cd /var/www/html/sr0/ && ln -s /media/cdrom0 0
cd /var/www/html/sr3/ && ln -s /media/cdrom3 3
```

```
cd /var/www/html/sr0/ && dpkg-scanpackages . /dev/null | gzip -9c > Packges.gz
cd /var/www/html/sr1/ && dpkg-scanpackages . /dev/null | gzip -9c > Packges.gz
cd /var/www/html/sr2/ && dpkg-scanpackages . /dev/null | gzip -9c > Packges.gz
cd /var/www/html/sr3/ && dpkg-scanpackages . /dev/null | gzip -9c > Packges.gz
```

### TFTP

apt install tftpd-hpa

nano /etc/default/tftpd-hpa

```
TFTP_USERNAME="root" 
TFTP_DIRECTORY="/srv/tftp" 
TFTP_ADDRESS="0.0.0.0:69" 
TFTP_OPTIONS="--secure --create"
```

sudo chown -R $USER /srv/tftp


