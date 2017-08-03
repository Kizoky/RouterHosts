## This is a simple repo for use of different hosts files

I think i'm not the only one who hates every single ADs on the internet
and with Adblocker is not itself anymore, that won't take away all ads

## How to use

For dummies, I suggest searching on the internet on how to figure out making a script run at only once per reboot, or If you wish
per hours or days.

If your (custom) firmware can do this, then just paste this command:
Make sure dnsmasq is reading hosts file or else the ads won't go away.
Also make sure your router has enough storage to store the hosts file, usually 24mb won't be enough.

```xml
wget http://winhelp2002.mvps.org/hosts.txt -O /etc/storage/dnsmasq/hosts
cat /etc/storage/dnsmasq/hosts >> /etc/hosts
wget https://adaway.org/hosts.txt -O /etc/storage/dnsmasq/hosts
cat /etc/storage/dnsmasq/hosts >> /etc/hosts
wget http://www.hostsfile.org/Downloads/hosts.txt -O /etc/storage/dnsmasq/hosts
cat /etc/storage/dnsmasq/hosts >> /etc/hosts
wget https://github.com/Kizoky/RouterHosts/blob/master/hosts1.txt -O /etc/storage/dnsmasq/hosts
cat /etc/storage/dnsmasq/hosts >> /etc/hosts
killall dnsmasq
dnsmasq
```

## Alternative way If your router has a huge storage
Make sure your dnsmasq.conf is configured to read these hosts (hosts1;hosts2;hosts3)

```xml
killall dnsmasq
wget http://winhelp2002.mvps.org/hosts.txt -O /etc/storage/dnsmasq/hosts3
wget https://adaway.org/hosts.txt -O /etc/storage/dnsmasq/hosts1
wget http://www.hostsfile.org/Downloads/hosts.txt -O /etc/storage/dnsmasq/hosts2
sleep 7
dnsmasq
```
