apt install tftpd-hpa

nano /etc/default/tftpd-hpa

```
TFTP_USERNAME="root" 
TFTP_DIRECTORY="/srv/tftp" 
TFTP_ADDRESS="0.0.0.0:69" 
TFTP_OPTIONS="--secure --create"
```

sudo chown -R $USER /srv/tftp