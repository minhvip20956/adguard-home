## 1. Setup Adguard Home:

**a) Ubuntu/Debian amd64 Server**

```Text
cd /
apt install sudo nano bind9-host wget -y
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz
tar -xvf AdGuardHome_linux_amd64.tar.gz
rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
./AdGuardHome -s install
```

**b) Ubuntu/Debian/Armbian arm64 Server**

```Text
cd /
apt install sudo nano bind9-host wget -y
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm64.tar.gz
tar -xvf AdGuardHome_linux_arm64.tar.gz
rm AdGuardHome_linux_arm64.tar.gz
cd /AdGuardHome/
./AdGuardHome -s install
```

**c) Raspberry Pi (32-bit ARMv6) Server**

```Text
cd /
apt install sudo nano bind9-host wget -y
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm.tar.gz
tar -xvf AdGuardHome_linux_arm.tar.gz
rm AdGuardHome_linux_arm.tar.gz
cd /AdGuardHome/
./AdGuardHome -s install
```

**c) CentOS amd64 Server**

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
yum install nano bind9-host wget -y
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz
tar -xvf AdGuardHome_linux_amd64.tar.gz
rm AdGuardHome_linux_amd64.tar.gz
cd /AdGuardHome/
./AdGuardHome -s install
```

## 2. Setup AdGuard Home Basic:

**a) Finish Setup: http://{YOUR-IP-ADDRESS}:3000**

Please complete installation with default settings

**b) Open Port:**

- Manager HTTP: 80 (TCP - UDP)

- Manager HTTPS: 443 (TCP - UDP)

- Public DNS: 53 (TCP - UDP, without DNSSEC)

- DoT DNS: tls://{YOUR-DOMAIN}:853 (TCP)

- DoH DNS: https://{YOUR-DOMAIN}/dns-query (Same location with Manager HTTPS)

**c) Set time zone**

```Text
sudo dpkg-reconfigure tzdata
```

**d) Set up SSL**

```Text
sudo apt install certbot -y
certbot -d domain.ltd --manual --preferred-challenges dns certonly
```

**e) Crontab**

```Text
crontab -e
```

- For Ubuntu

```Text
50 4 * * * apt update -y && apt upgrade -y && apt autoremove -y && reboot
00 00 * * * certbot renew --manual-auth-hook /etc/letsencrypt/renewal-hooks/pre/dnsauthenticator.sh
```

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

## 4. Allow Lists:

```Text
https://raw.githubusercontent.com/AdguardTeam/AdGuardSDNSFilter/master/Filters/exclusions.txt
https://raw.githubusercontent.com/minhvip20956/AdBlockList/master/list/allow.txt
https://github.com/EnergizedProtection/unblock/raw/master/basic/formats/domains.txt
```

## 5. DNS Rewrite:

```Text
172.217.1.14	manifest.googlevideo.com
```

(https://www.reddit.com/r/pihole/comments/9w5swx/i_think_ive_managed_to_block_youtube_ads_with/)
