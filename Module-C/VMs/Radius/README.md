nano /etc/apt/sources.list

```
deb [trusted=yes] http://127.0.0.1/sr0/ ./
deb [trusted=yes] http://127.0.0.1/sr1/ ./
deb [trusted=yes] http://127.0.0.1/sr2/ ./
deb [trusted=yes] http://127.0.0.1/sr3/ ./
```

apt updade

### Radius

apt install freeradius

nano /etc/freeradius/3.0/clients.conf

```
client localhost {
****
        secret = Passw0rd!
****
}

client LODZ1 {
        ipaddr          = lodz1.lodz.pl
        secret          = Passw0rd!
}
client LODZ2 {
        ipaddr          = lodz2.lodz.pl
        secret          = Passw0rd!
}
```

nano /etc/freeradius/3.0/users

```
super           Cleartext-Password := "Passw0rd!"
                cisco-avpair    = "shell:priv-lvl=15"

regular         Cleartext-Password := "Passw0rd!"
                cisco-avpair    = "shell:priv-lvl=1"
```

nano /etc/freeradius/3.0/sites-available/default

```
# IPv4 versions
listen {
****
        type = auth
        port = 1645
****
}
listen {
****
        port = 1646
        type = acct
****
}
# IPv6 versions
listen {
****
        type = auth
        port = 1645
****
}
listen {
****
        port = 1646
        type = acct
****
}
```