![AdGuardHome Banner](/bg.jpg)

## 1. Setup Adguard Home:

**a) Ubuntu amd64 Server**

```Text
cd /
sudo apt install sudo nano bind9-host wget -y
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz
sudo rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
sudo ./AdGuardHome -s install
```

**b) Ubuntu/Armbian arm64 Server**

```Text
cd /
sudo apt install sudo nano bind9-host wget -y
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm64.tar.gz
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz
sudo rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
sudo ./AdGuardHome -s install
```

**c) Raspbian arm86 Server**

```Text
cd /
sudo apt install sudo nano bind9-host wget -y
sudo wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm.tar.gz
sudo tar -xvf AdGuardHome_linux_amd64.tar.gz
sudo rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
sudo ./AdGuardHome -s install
```

**c) CentOS amd64 Server(with Root Address)**

```Text
firewall-cmd --zone=public --permanent --add-port 80/tcp
firewall-cmd --zone=public --permanent --add-port 80/udp
firewall-cmd --zone=public --permanent --add-port 443/tcp
firewall-cmd --zone=public --permanent --add-port 443/udp
firewall-cmd --zone=public --permanent --add-port 53/tcp
firewall-cmd --zone=public --permanent --add-port 53/udp
firewall-cmd --zone=public --permanent --add-port 853/tcp
firewall-cmd --zone=public --permanent --add-port 3000/tcp
firewall-cmd --reload
cd /
yum install epel-release -y
yum install nano bind9-host wget -y
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz
tar -xvf AdGuardHome_linux_amd64.tar.gz
rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
./AdGuardHome -s install
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
sudo apt install certbot -y
certbot -d domain.ltd --manual --preferred-challenges dns certonly
```

- For CentOS

```Text
yum install epel-release -y
sudo apt install certbot -y
certbot -d domain.ltd --manual --preferred-challenges dns certonly
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

![AdGuardHome Image2](/home2.jpg)

## 3. Block Filters List:

**a) Default List (Recommended):**

```Text
https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt
https://adaway.org/hosts.txt
https://www.malwaredomainlist.com/hostslist/hosts.txt
```

**b) Selection list (Recommended):**

```Text
https://filters.adtidy.org/extension/chromium/filters/15.txt
https://dbl.oisd.nl/
https://abpvn.com/android/abpvn.txt
https://raw.githubusercontent.com/bigdargon/hostsVN/master/option/domain.txt
https://raw.githubusercontent.com/BlackJack8/iOSAdblockList/master/Hosts.txt
https://v.firebog.net/hosts/static/w3kbl.txt
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext
https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt
https://mirror1.malwaredomains.com/files/justdomains
https://v.firebog.net/hosts/Prigent-Malware.txt
https://mirror.cedia.org.ec/malwaredomains/immortal_domains.txt
https://www.dshield.org/feeds/suspiciousdomains_Low.txt
https://raw.githubusercontent.com/StevenBlack/hosts/master/alternates/fakenews-gambling-social/hosts
https://gitlab.com/EnergizedProtection/block/raw/master/ultimate/formats/hosts
https://raw.githubusercontent.com/kboghdady/youTube_ads_4_pi-hole/master/black.list
https://raw.githubusercontent.com/HenningVanRaumle/pihole-ytadblock/master/ytadblock.txt
```

![AdGuardHome Image3](/home3.jpg)

## 4. Allow Lists:

```Text
https://raw.githubusercontent.com/AdguardTeam/AdGuardSDNSFilter/master/Filters/exclusions.txt
https://raw.githubusercontent.com/minhvip20956/AdBlockList/master/list/allow.txt
https://github.com/EnergizedProtection/unblock/raw/master/basic/formats/domains.txt
```

![AdGuardHome Image4](/deve.png)

## 5. Edit "AdGuardHome.yaml" (For Advanced):

**a) Open "AdGuardHome.yaml" file with Nano:***

```Text
cd /AdGuardHome/
nano AdGuardHome.yaml
```

**b) "AdGuardHome.yaml" optimization:***

- Add the amount of DNS buffer (This option depends on the amount of free RAM on your server), find "cache_size:" and edit:

```Text
128 MB = 134217728 (Recommended, For 1GB RAM Server)
256 MB = 268435456 (For 1,5GB RAM Server)
1024 MB = 1073741824 (For 2GB RAM Server)
```

- Other ENV:

```Text
  cache_ttl_min: 3600
  cache_ttl_max: 86400
  safebrowsing_cache_size: 134217728  
```

After setting. Type the following command to restart AdGuard

```Text
./ AdGuardHome -s restart
```
