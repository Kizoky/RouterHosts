## This is a simple repo on how to block ads on padavan firmwares

I have many devices that are still unrooted, or the bootloader can't be unlocked
As a result I blocked all ads on the router instead, this way every PC or phones/tablets won't slow down

## How to use

Make sure dnsmasq is reading /tmp/hosts file or else the ads won't go away.
LAN -> DHCP Server
Custom Configuration File "dnsmasq.conf"
```xml
addn-hosts=/tmp/hosts
```
Advanced Settings -> Customization -> Scripts -> Run After Router Started:
 Then just copy and paste this into the end of that box

```xml
touch /tmp/hosts
sleep 8
logger "download Zero hosts file..." && wget -qO- "http://someonewhocares.org/hosts/zero/hosts" | awk -v r="0.0.0.0" '{sub(/^0.0.0.0/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download MVPS hosts file..." && wget -qO- "http://winhelp2002.mvps.org/hosts.txt" | awk -v r="0.0.0.0" '{sub(/^0.0.0.0/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download AdAway blocklist hosts file..." && wget -qO- "https://adaway.org/hosts.txt" |awk -v r="0.0.0.0" '{sub(/^127.0.0.1/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download MalwareDomainList hosts file..." && wget -qO- "https://www.malwaredomainlist.com/hostslist/hosts.txt" |awk -v r="0.0.0.0" '{sub(/^127.0.0.1/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download hpHosts hosts file..." && wget -qO- "http://hosts-file.net/ad_servers.txt" |awk -v r="0.0.0.0" '{sub(/^127.0.0.1/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download Ad server hosts file..." && wget -qO- "http://pgl.yoyo.org/adservers/serverlist.php?hostformat=dnsmasq&showintro=0&mimetype=plaintext" |awk -v r="0.0.0.0" '{sub(/^127.0.0.1/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "download Kizoky hosts file..." && wget -qO- "https://raw.githubusercontent.com/Kizoky/RouterHosts/master/hosts1.txt" |awk -v r="0.0.0.0" '{sub(/^127.0.0.1/, r)} $0 ~ "^"r' >> /tmp/temp-hosts
logger "Updating /tmp/hosts file..." && cat /tmp/temp-hosts | sort -uk2 >> /tmp/hosts
rm /tmp/temp-hosts && logger "/tmp/hosts file has been successfully updated."
killall -SIGHUP dnsmasq
```
Then reboot your router.
Check the logs when the router is up again, and you should see messages like
```xml
May 29 22:48:14 admin: download Zero hosts file...
May 29 22:48:26 admin: download MVPS hosts file...
May 29 22:48:29 admin: download AdAway blocklist hosts file...
May 29 22:48:30 admin: download MalwareDomainList hosts file...
May 29 22:48:45 admin: download hpHosts hosts file...
May 29 22:48:54 admin: download Ad server hosts file...
May 29 22:48:55 admin: download Kizoky hosts file...
May 29 22:49:04 admin: Updating /tmp/hosts file...
May 29 22:49:07 admin: /tmp/hosts file has been successfully updated.
```

And finally If you did it right you should be able to see this message along:
```xml
May 29 22:53:50 dnsmasq[520]: read /tmp/hosts - 117937 addresses
```

