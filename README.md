1) Disable SELINUX (edit /etc/selinux/config) and reboot
2) Update your CentOS installation and reboot if necessary
```bash
yum -y update
```
3) Add Atomicorp repo (see https://wiki.atomicorp.com/wiki/index.php/Atomic)
```bash
wget -q -O - https://www.atomicorp.com/installers/atomic | sh
```
4) Install the follow packages
```bash
yum install -y wget bzip2 texlive net-tools alien gnutls-utils
```
5) Install OpenVAS 9
```bash
yum install openvas -y
```
6) edit /etc/redis.conf. Add/uncomment the following
```bash
unixsocket /tmp/redis.sock
unixsocketperm 700
```
7) Restart Redis
```bash
systemctl enable redis && systemctl restart redis
```
8) Follow instructions and remember your admin password. If rsync throws error, check that your network allows outgoing TCP 873 to internet
```bash
openvas-setup
```
9) Open firewall port for tcp/9392
```bash
firewall-cmd --permanent --add-port=9392/tcp
firewall-cmd --reload
firewall-cmd --list-port
```

Go to:
```bash
https://<IP-ADDRESS>:9392 and login.
```
10) To verify your OpenVAS setup, run
```bash
openvas-check-setup --v9
```

Related link:
https://forums.atomicorp.com/viewtopic.php?f=31&t=8539#p44057
