![AdGuardHome Banner](/home2.jpg)

## 1. Setup Adguard Home:

**a) Ubuntu amd64 Server**

```Text
cd /;\
sudo apt install sudo nano bind9-host wget -y;\
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz;\
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz;\
sudo rm -f AdGuardHome_linux_amd64.tar.gz;\
cd /AdGuardHome/;\
sudo ./AdGuardHome -s install;\
```

**b) Ubuntu/Armbian arm64 Server**

```Text
cd /;\
sudo apt install sudo nano bind9-host wget -y;\
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm64.tar.gz;\
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz;\
sudo rm -f AdGuardHome_linux_amd64.tar.gz;\
cd /AdGuardHome/;\
sudo ./AdGuardHome -s install;\
```

**c) Raspbian arm86 Server**

```Text
cd /
sudo apt install sudo nano bind9-host wget -y;\
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm.tar.gz;\
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz;\
sudo rm -f AdGuardHome_linux_amd64.tar.gz;\
cd /AdGuardHome/;\
sudo ./AdGuardHome -s install;\
```

**c) CentOS amd64 Server (Access Root account)**

```Text
firewall-cmd --zone=public --permanent --add-port 22/tcp;\
firewall-cmd --zone=public --permanent --add-port 80/tcp;\
firewall-cmd --zone=public --permanent --add-port 80/udp;\
firewall-cmd --zone=public --permanent --add-port 443/tcp;\
firewall-cmd --zone=public --permanent --add-port 443/udp;\
firewall-cmd --zone=public --permanent --add-port 53/tcp;\
firewall-cmd --zone=public --permanent --add-port 53/udp;\
firewall-cmd --zone=public --permanent --add-port 853/tcp;\
firewall-cmd --zone=public --permanent --add-port 853/udp;\
firewall-cmd --zone=public --permanent --add-port 3000/tcp;\
firewall-cmd --zone=public --permanent --add-port 44444/tcp;\
firewall-cmd --zone=public --permanent --add-port 55555/tcp;\
firewall-cmd --reload;\
cd /;\
yum clean all;\
yum update -y;yum upgrade -y;yum autoremove -y;\
yum install epel-release -y;\
yum update -y;yum upgrade -y;yum autoremove -y;\
yum install nano bind9-host wget -y;\
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz;\
tar -xvf AdGuardHome_linux_amd64.tar.gz;\
rm -f AdGuardHome_linux_amd64.tar.gz;\
cd /AdGuardHome/;\
./AdGuardHome -s install;\
```

![AdGuardHome Image1](/home1.png)

## 2. Setup AdGuard Home and Server Basic:

**a) Finish Setup: http://{YOUR-IP-ADDRESS}:3000**

Please complete the installation with the default settings. Make sure ports 80 and 53 are not occupied!!!

**b) Open the ports (if your server is behind a firewall. Ignore if it is an internal server):**

- Manager HTTP: 80 (TCP - UDP)

- Manager HTTPS: 443 (TCP - UDP)

- Public DNS: 53 (TCP - UDP, without DNSSEC (Support DNSSEC after Enable in Setting))

- DoT DNS: tls://{YOUR-DOMAIN}:853 (TCP)

- DoH DNS: https://{YOUR-DOMAIN}/dns-query (Same location with Manager HTTPS)

**c) Set time zone (for Crontab)**

```Text
sudo dpkg-reconfigure tzdata
```

**d) Set up SSL (if you want used Dot/DoH DNS Option and Secure Setup Page)**

- For Ubuntu/Raspbian/Debian/Armbian

```Text
sudo apt install certbot -y;\
certbot -d domain.ltd --manual --preferred-challenges dns certonly;\
```

- For CentOS

```Text
yum install epel-release -y;\
sudo apt install certbot -y;\
certbot -d domain.ltd --manual --preferred-challenges dns certonly;\
```

Replace domain.ltd with your domain name. Please A Record to your server.

This command will run the DNS challenge for you. Refer to how to overcome DNS challenges here: https://certbot.eff.org/docs/using.html#manual

After passing the DNS challenge, you will be provided with the location to save the necessary PEM files of the following form:

```Text
/etc/letsencrypt/live/{domain.ltd}/fullchain.pem

/etc/letsencrypt/live/{domain.ltd}/privkey.pem
```

Please add each of the location one by one to AdGuardHome's settings.

**e) Crontab (Renew SSL every day and auto update and reboot server at 4:50AM)**

```Text
crontab -e
```

- For Ubuntu/Raspbian/Debian/Armbian

```Text
50 4 * * * apt update -y && apt upgrade -y && apt autoremove -y && reboot
00 00 * * * certbot renew --manual-auth-hook /etc/letsencrypt/renewal-hooks/pre/dnsauthenticator.sh
```

- For CentOS

```Text
50 4 * * * yum update -y && yum upgrade -y && yum autoremove -y && reboot
00 00 * * * certbot renew --manual-auth-hook /etc/letsencrypt/renewal-hooks/pre/dnsauthenticator.sh
```

![AdGuardHome Image2](/bg.jpg)

## 3. Block Filters List:

```Text
https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt
https://raw.githubusercontent.com/AdAway/adaway.github.io/master/hosts.txt
https://www.malwaredomainlist.com/hostslist/hosts.txt
https://someonewhocares.org/hosts/zero/hosts
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/GameConsoleAdblockList.txt
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV-AGH.txt
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=adblockplus&showintro=1&mimetype=plaintext
https://raw.githubusercontent.com/hoshsadiq/adblock-nocoin-list/master/nocoin.txt
https://raw.githubusercontent.com/durablenapkin/scamblocklist/master/adguard.txt
https://raw.githubusercontent.com/Spam404/lists/master/main-blacklist.txt
https://raw.githubusercontent.com/mitchellkrogza/The-Big-List-of-Hacked-Malware-Web-Sites/master/hacked-domains.list
https://anti-ad.net/easylist.txt
https://raw.githubusercontent.com/DRSDavidSoft/additional-hosts/master/domains/blacklist/unwanted-iranian.txt
https://filtri-dns.ga/filtri.txt
https://280blocker.net/files/280blocker_domain.txt
https://raw.githubusercontent.com/yous/YousList/master/hosts.txt
https://raw.githubusercontent.com/cchevy/macedonian-pi-hole-blocklist/master/hosts.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/NorwegianExperimentalList%20alternate%20versions/NordicFiltersAdGuardHome.txt
https://raw.githubusercontent.com/MajkiIT/polish-ads-filter/master/polish-pihole-filters/hostfile.txt
https://raw.githubusercontent.com/lassekongo83/Frellwits-filter-lists/master/Frellwits-Swedish-Hosts-File.txt
https://raw.githubusercontent.com/xorcan/hosts/master/xhosts.txt
https://abpvn.com/android/abpvn.txt
https://dbl.oisd.nl/
https://raw.githubusercontent.com/minhvip20956/AdBlockList/master/list/block.txt
https://raw.githubusercontent.com/anudeepND/blacklist/master/CoinMiner.txt
https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt
https://raw.githubusercontent.com/anudeepND/blacklist/master/facebook.txt
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
https://mirror1.malwaredomains.com/files/justdomains
http://sysctl.org/cameleon/hosts
https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
```

![AdGuardHome Image3](/home3.jpg)

## 4. Allow Lists:

```Text
https://raw.githubusercontent.com/AdguardTeam/AdGuardSDNSFilter/master/Filters/exclusions.txt
https://raw.githubusercontent.com/minhvip20956/AdBlockList/master/list/allow.txt
https://raw.githubusercontent.com/anudeepND/whitelist/master/domains/whitelist.txt
```

![AdGuardHome Image4](/deve.png)
