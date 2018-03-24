# simple-dns-adblock
simple dns adblocker using dnsmasq

#### To install:

Install dnsmasq. Enable dnsmasq:

> sysrc dnsmasq_enable="YES"
> sysrc dnsmasq_flags="-R"

Create directory /usr/local/etc/dnsmasq.d/ with "nobody:nobody" permissions. 

Place the update_dnsmasq in /usr/local/bin/ (make it executable - chmod +x )

Add the following lines to /etc/crontab:
```
30      5       1       *       *       root    update_dnsmasq
30      5       1       *       *       root    service dnsmasq restart

Create this file (change as neccessary):
usr/local/etc/dnsmasq.d/simple-dns-block.conf 
```
#Config credit - Pi-Hole
addn-hosts=/usr/local/etc/dnsmasq.d/blocklist.txt

localise-queries

no-resolv

cache-size=10000

log-queries=extra
log-facility=/var/log/sdb.log

local-ttl=2

log-async
#open dns servers - change if needed
server=208.67.222.222
server=208.67.220.220
#change interface to match yours
interface=re1

Edit /usr/local/etc/dnsmasq.conf:
``
config-dir="/usr/local/etc/dnsmasq.d/"

Start dnsmasq:
> service dnsmasq start
