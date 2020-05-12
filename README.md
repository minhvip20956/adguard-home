## 1. Setup Adguard Home for Linux x64 Server

```Text
sudo apt install wget -y && wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz

tar -xvf AdGuardHome_linux_amd64.tar.gz

rm AdGuardHome_linux_amd64.tar.gz

cd /home/{User}/AdGuardHome/

sudo ./AdGuardHome -s install
```
Replace {User} with the personal directory name of the account you own

## 2. Setup AdGuard Home Basic

**a) Finish Setup: http://{YOUR-IP-ADDRESS}:3000**

Please complete installation with default settings

**b) Open Port:**

- http port: 80

- https port: 443

- DNS Port: 53 (TCP and UDP)

- TLS DNS: {YOUR-DOMAIN}:853 (TCP)

- HTTP DNS: https://{YOUR-DOMAIN}/dns-query

**c) Set time zone**

sudo dpkg-reconfigure tzdata

**d) Set up SSL**

sudo apt install certbot -y
certbot -d domain.ltd --manual --preferred-challenges dns certonly

**e) Crontab**

crontab -e

```Text
50 4 * * * apt update -y && apt upgrade -y && apt autoremove -y && reboot
00 00 * * * certbot renew --manual-auth-hook /etc/letsencrypt/renewal-hooks/pre/dnsauthenticator.sh
```

## 3. Block Filters List

**a) Default List (Recommended):**

```Text
https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt
https://adaway.org/hosts.txt
https://www.malwaredomainlist.com/hostslist/hosts.txt
```

**b) AdBlock Plus List (VIP Official List - Recommended):**

```Text
https://cdn.adblockcdn.com/filters/adblock_custom.txt
https://easylist-downloads.adblockplus.org/abp-filters-anti-cv.txt
https://easylist-downloads.adblockplus.org/easylist.txt
https://easylist-downloads.adblockplus.org/abpvn+easylist.txt
https://easylist-downloads.adblockplus.org/antiadblockfilters.txt
https://easylist-downloads.adblockplus.org/fanboy-social.txt
https://easylist-downloads.adblockplus.org/easyprivacy.txt
https://easylist-downloads.adblockplus.org/malwaredomains_full.txt
https://easylist-downloads.adblockplus.org/fanboy-annoyance.txt
https://easylist-downloads.adblockplus.org/easylist-cookie.txt
https://easylist-downloads.adblockplus.org/yt_annoyances_full.txt
https://easylist.to/easylistgermany/easylistgermany.txt
https://easylist-downloads.adblockplus.org/easylistitaly.txt
https://easylist-downloads.adblockplus.org/easylistdutch.txt
https://easylist-downloads.adblockplus.org/liste_fr.txt
https://easylist-downloads.adblockplus.org/easylistchina.txt
https://stanev.org/abp/adblock_bg.txt
https://raw.githubusercontent.com/heradhis/indonesianadblockrules/master/subscriptions/abpindo.txt
https://easylist-downloads.adblockplus.org/Liste_AR.txt
https://raw.githubusercontent.com/tomasko126/easylistczechandslovak/master/filters.txt
https://notabug.org/latvian-list/adblock-latvian/raw/master/lists/latvian-list.txt
https://raw.githubusercontent.com/easylist/EasyListHebrew/master/EasyListHebrew.txt
http://margevicius.lt/easylistlithuania.txt
https://easylist-downloads.adblockplus.org/easyprivacy.tpl
```

**c) AdGuard Chromium List (VIP Official List - Recommended):**

```Text
https://filters.adtidy.org/extension/chromium/filters/1.txt
https://filters.adtidy.org/extension/chromium/filters/2.txt
https://filters.adtidy.org/extension/chromium/filters/3.txt
https://filters.adtidy.org/extension/chromium/filters/4.txt
https://filters.adtidy.org/extension/chromium/filters/6.txt
https://filters.adtidy.org/extension/chromium/filters/7.txt
https://filters.adtidy.org/extension/chromium/filters/8.txt
https://filters.adtidy.org/extension/chromium/filters/9.txt
https://filters.adtidy.org/extension/chromium/filters/11.txt
https://filters.adtidy.org/extension/chromium/filters/12.txt
https://filters.adtidy.org/extension/chromium/filters/13.txt
https://filters.adtidy.org/extension/chromium/filters/14.txt
https://filters.adtidy.org/extension/chromium/filters/15.txt
https://filters.adtidy.org/extension/chromium/filters/16.txt
https://easylist.to/easylist/easylist.txt
https://easylist.to/easylist/easyprivacy.txt
https://easylist.to/easylist/fanboy-annoyance.txt
https://raw.githubusercontent.com/yourduskquibbles/webannoyances/master/ultralist.txt
https://www.i-dont-care-about-cookies.eu/abp/
https://raw.githubusercontent.com/reek/anti-adblock-killer/master/anti-adblock-killer-filters.txt
https://raw.githubusercontent.com/liamja/Prebake/master/obtrusive.txt
https://raw.githubusercontent.com/hoshsadiq/adblock-nocoin-list/master/hosts.txt
```

*** The 5 and 10 filters I left out because it was the parasite that allowed advertising and test filters. Please do not add.

**d)  OISD.NL List (High Recommended):**

```Text
https://dbl.oisd.nl/
```

**e) FANBOY Lists (Optional):**

```Text
https://fanboy.co.nz/enhancedstats.txt
https://www.fanboy.co.nz/fanboy-cookiemonster.txt
https://www.fanboy.co.nz/fanboy-problematic-sites.txt
https://easylist.to/easylist/fanboy-social.txt
```

**f) VietNam Lists (Optional):**

```Text
https://abpvn.com/android/abpvn.txt
https://raw.githubusercontent.com/bigdargon/hostsVN/master/option/domain.txt
```

**g) Other Lists by AdGuard (Optional):**

```Text
https://raw.githubusercontent.com/hoshsadiq/adblock-nocoin-list/master/nocoin.txt
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV-AGH.txt
https://raw.githubusercontent.com/durablenapkin/scamblocklist/master/adguard.txt
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=adblockplus&showintro=1&mimetype=plaintext
https://ssl.bblck.me/blacklists/domain-list.txt
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/StreamingAds/hosts
https://someonewhocares.org/hosts/zero/hosts
https://raw.githubusercontent.com/mitchellkrogza/The-Big-List-of-Hacked-Malware-Web-Sites/master/hacked-domains.list
https://raw.githubusercontent.com/Spam404/lists/master/main-blacklist.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/GameConsoleAdblockList.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/NorwegianExperimentalList%20alternate%20versions/NordicFiltersAdGuardHome.txt
https://raw.githubusercontent.com/MajkiIT/polish-ads-filter/master/polish-pihole-filters/hostfile.txt
https://raw.githubusercontent.com/yous/YousList/master/hosts.txt
https://raw.githubusercontent.com/lassekongo83/Frellwits-filter-lists/master/Frellwits-Swedish-Hosts-File.txt
https://filtri-dns.ga/filtri.txt
https://280blocker.net/files/280blocker_domain.txt
https://raw.githubusercontent.com/w13d/adblockListABP-PiHole/master/list.txt
https://raw.githubusercontent.com/DRSDavidSoft/additional-hosts/master/domains/blacklist/unwanted-iranian.txt
https://raw.githubusercontent.com/deletescape/noads/master/lists/add-switzerland.txt
https://raw.githubusercontent.com/cchevy/macedonian-pi-hole-blocklist/master/hosts.txt
```

**h) Other Lists (Optional):**

```Text
https://raw.githubusercontent.com/Dawsey21/Lists/master/adblock-list.txt
https://raw.githubusercontent.com/paulgb/BarbBlock/master/blacklists/adblock-plus.txt
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
https://mirror1.malwaredomains.com/files/justdomains
http://sysctl.org/cameleon/hosts
https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
https://www.dshield.org/feeds/suspiciousdomains_Low.txt
https://raw.githubusercontent.com/kboghdady/youTube_ads_4_pi-hole/master/black.list
https://jasonhill.co.uk/pfsense/ytadblock.txt
https://raw.githubusercontent.com/HenningVanRaumle/pihole-ytadblock/master/ytadblock.txt
https://raw.githubusercontent.com/HenningVanRaumle/pihole-ytadblock/master/googlevideo.com%20domains/adverisment.txt
https://raw.githubusercontent.com/BlackJack8/iOSAdblockList/master/Hosts.txt
```


## 4. Allow Lists:

```Text
https://raw.githubusercontent.com/AdguardTeam/AdGuardSDNSFilter/master/Filters/exclusions.txt
https://raw.githubusercontent.com/minhvip20956/AdBlockList/master/list/allow.txt
```

## 5. DNS Rewrite:

```Text
172.217.1.14	manifest.googlevideo.com
```

(https://www.reddit.com/r/pihole/comments/9w5swx/i_think_ive_managed_to_block_youtube_ads_with/)
