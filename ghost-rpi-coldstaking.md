# RaspberryPi Cold Staking Setup
Here you will find information about how you can set up a cold staking RasperryPi for the Ghost network. This will allow you to stake your coins continuously on your own "Staking Server" and Privacy-Network-Node under your controll to maximize earnings from staking rewards.

- [Heading](#heading)
  * [Sub-heading](#sub-heading)
    + [Sub-sub-heading](#sub-sub-heading)
- [Heading](#heading-1)
  * [Sub-heading](#sub-heading-1)
    + [Sub-sub-heading](#sub-sub-heading-1)
- [Heading](#heading-2)
  * [Sub-heading](#sub-heading-2)
    + [Sub-sub-heading](#sub-sub-heading-2)

  

## RaspberryPi setup
For this guide we will be using:
### Hardware to prepare
* RaspberryPi2 - but any should work
* SD-Card - 16GB+ !Backup is as large as the SD-Card!
* Power Supply - use appropriate one

### Software to prepare
* Raspberry Imager https://www.raspberrypi.org/downloads/
![RaspberryImager](https://github.com/chmess/guides/blob/master/Imager.png?raw=true)

* PuTTY https://www.putty.org/
  * direct download Link for Windows: https://the.earth.li/~sgtatham/putty/latest/w32/putty.exe


### Setup
1. put SD Card in Slot of your Desktop
2. install & run  RaspberyPi Imager (choose your SD Card & Operating System)
![RaspberryImager2](https://github.com/chmess/guides/blob/master/Imager2.png?raw=true)
3. Press Write
4. Wait ;)
5. Remove SD Card
steps 6.-11. only needed when you will use WiFi and login over Network
6. re-insert SD Card
7. open SD Card in Windows File Explorer
8. create empty Textfile and name it "ssh" without .extention (right-click) 
![FileExplorer1](https://github.com/chmess/guides/blob/master/pissh1.png?raw=true)
![FileExplorer2](https://github.com/chmess/guides/blob/master/pissh2.png?raw=true)
9. create a text file called "wpa_supplicant.conf"
10. edit wpa_supplicant.conf, insert text with your WiFi Credecials:
![FileExplorer3](https://github.com/chmess/guides/blob/master/pissh3.png?raw=true)
```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
scan_ssid=1
ssid="your_wifi_ssid"
psk="your_wifi_password"
}
```
11. eject SD Card
12. insert SD Card in RaspberryPi
13. Power Up RaspberryPi
this will take a minute, you can watch with a HDMI Monitor
14. start Putty 
    * Host Name: raspberrypi
    * Connection type SSH
    * click Open

![FileExplorer4](https://github.com/chmess/guides/blob/master/pissh4.png?raw=true)

15. yes to security things
it will only appear once and its telling you there is a new SSH-Key
16. login with 
```
user = pi 
password = raspberry
```
![FileExplorer5](https://github.com/chmess/guides/blob/master/pissh5.png?raw=true)

17. change Password as adviced
type "passwd"[enter] and change it to password of your choice
18. Add  User ghost
```
sudo adduser ghost
sudo usermod ghost -a -G pi,adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev
```
19. Login as ghost and your password(step 14+16)
20. install Ghostman https://github.com/ghost-coin/ghostman
```
sudo apt-get install python git unzip pv jq dnsutils
```
this will install all necassary packages for Ghostman
when promptet answer "y"
```
cd ~ && git clone https://github.com/ghost-coin/ghostman
```
this will clone the Ghost software from GitHub to ghost home directory
```
cd ~/ghostman 
```
change to new ghostman directory
```
bash quicksetup.sh
```
start setup-script
```
ghost@raspberrypi:~ $ cd ghostman/
ghost@raspberrypi:~/ghostman $ bash quicksetup.sh
[sudo] Passwort für ghost:
Holen:1 http://raspbian.raspberrypi.org/raspbian buster InRelease [15,0 kB]
OK:2 https://download.docker.com/linux/raspbian buster InRelease
Holen:3 http://archive.raspberrypi.org/debian buster InRelease [32,6 kB]
Holen:4 http://raspbian.raspberrypi.org/raspbian buster/main armhf Packages [13,0 MB]
Holen:5 http://archive.raspberrypi.org/debian buster/main armhf Packages [330 kB]
Es wurden 13,4 MB in 8 s geholt (1.710 kB/s).
Paketlisten werden gelesen... Fertig
Abhängigkeitsbaum wird aufgebaut.
Statusinformationen werden eingelesen.... Fertig
Aktualisierung für 27 Pakete verfügbar. Führen Sie »apt list --upgradable« aus, um sie anzuzeigen.
Paketlisten werden gelesen... Fertig
Abhängigkeitsbaum wird aufgebaut.
Statusinformationen werden eingelesen.... Fertig
dnsutils ist schon die neueste Version (1:9.11.5.P4+dfsg-5.1+deb10u1).
git ist schon die neueste Version (1:2.20.1-2+deb10u3).
jq ist schon die neueste Version (1.5+dfsg-2+b1).
pv ist schon die neueste Version (1.6.6-1).
python ist schon die neueste Version (2.7.16-1).
unzip ist schon die neueste Version (6.0-23+deb10u1).
Die folgenden Pakete wurden automatisch installiert und werden nicht mehr benötigt:
  libmicrodns0 rpi-eeprom-images
Verwenden Sie »sudo apt autoremove«, um sie zu entfernen.
0 aktualisiert, 0 neu installiert, 0 zu entfernen und 27 nicht aktualisiert.
ghostman version 0.12 - Di 14. Jul 20:36:04 BST 2020
gathering info, please wait...   done!
download https://github.com/ghost-coin/ghost-core/releases/download/v0.19.1.6/ghost-0.19.1.6-arm-linux-gnueabihf.tar.gz
and install to /home/ghost/ghostcore? [y/N] y                                                                                       done!
 --> Checksumming ghost-0.19.1.6-arm-linux-gnueabihf.tar.gz...  done!
 --> Unpacking ghost-0.19.1.6-arm-linux-gnueabihf.tar.gz...  done!
 --> adding /home/ghost/ghostcore PATH to ~/.bash_aliases ...  done!

Ghost 0.19.1.6 successfully installed!

Installed in /home/ghost/ghostcore

ls: Zugriff auf 'ghost-qt' nicht möglich: Datei oder Verzeichnis nicht gefunden
-rw-r--r-- 1 ghost ghost 34466399 Jul 14 20:36 ghost-0.19.1.6-arm-linux-gnueabihf.tar.gz
-rw-r--r-- 1 ghost ghost    98591 Jul 14 20:36 ghost-0.19.1.6-arm-linux-gnueabihf.tar.gz.DIGESTS.txt
lrwxrwxrwx 1 ghost ghost       18 Jul 14 20:36 ghost-cli -> ghost-cli-0.19.1.6
-rwxr-xr-x 1 ghost ghost  1896760 Jul  2 01:14 ghost-cli-0.19.1.6
lrwxrwxrwx 1 ghost ghost       15 Jul 14 20:36 ghostd -> ghostd-0.19.1.6
-rwxr-xr-x 1 ghost ghost  9382752 Jul  2 01:14 ghostd-0.19.1.6


To start ghostd run:

    ghostman restart now

Exiting.

ghostman version 0.12 - Di 14. Jul 20:36:28 BST 2020
 --> Deleting cache files, debug.log...  /home/ghost/.ghost/  done!
 --> Starting ghostd...  done!
 --> Waiting for ghostd to respond... .. done!
 --> ghost-cli getinfo
{
  "version": 19010600,
  "protocolversion": 90011,
  "blocks": 1738,
  "timeoffset": 0,
  "connections": 10,
  "proxy": "",
  "difficulty": 1898722.005695329,
  "chain": "main",
  "walletversion": 169900,
  "balance": 0.00000000,
  "keypoololdest": 1594755399,
  "keypoolsize": 0,
  "paytxfee": 0.00000000,
  "relayfee": 0.00001000,
  "warnings": ""
}

Exiting.

mkdir: das Verzeichnis „tmp“ kann nicht angelegt werden: Die Datei existiert bereits
ghostman version 0.12 - Di 14. Jul 20:36:39 BST 2020
gathering info, please wait...   done!
null
 --> checking wallet ...  done!

 --> recovery phrase : This is your recovery phrase for cold staking you will not need it but wright it down anyhow

Have you written down your recovery phrase?
 [y/N] y
 --> creating wallet ...  done!

    ghostman stakingnode info

Exiting.

ghostman version 0.12 - Di 14. Jul 20:37:56 BST 2020
gathering info, please wait...   done!
 --> checking wallet ...  done!

Create new staking node public key? [y/N] y
Label for new key : HowTo_RPi

 --> creating new cold staking public key ... PGHSTWtp8TtvrvSB6xdhAe1m9ZY7Byntsb4gHu4mbZkFz31v1v67H9VvVJAYi6ygtDvsxoWmnGdzG8Ey786kw8V58jTvQJYmAgiH5dy7fG5u8cf1

Exiting.

ghost@raspberrypi:~/ghostman $
```

21. Your Cold staking Node is ready to run
    * You can check GhostmanStatus with:
```
bash /~/ghostman/bin/ghostman.sh status
```
```
ghost@raspberrypi:~/ghostman/bin $ bash ghostman.sh status
ghostman version 0.12 - Di 14. Jul 21:56:53 CEST 2020
gathering info, please wait...   done!

  hostname                         : raspberrypi
  host uptime/load average         : 4 days, 0.16 0.03 0.01
  ghostd bind ip address         : 84.142.179.153
  ghostd version                 : 0.19.1.6
  ghostd up-to-date              : YES
  ghostd running                 : YES
  ghostd uptime                  : 5 hours 5 minutes
  ghostd responding        (RPC) : YES
  ghostd listening          (IP) : YES
  ghostd port open   (P2P 51728) : NO*
  ghostd connecting      (peers) : YES
  ghostd connection count        : 24
  ghostd blocks synced           : YES
  last block      (local ghostd) : 14363
             (ghostscan.io) : 14363
                          (chainz) : /home/ghost/ghostman/lib/functions.sh: Zeile 1535: [: : Ganzzahliger Ausdruck erwartet.

  ghostd staking enabled         : YES - 0%
  ghostd staking difficulty      : 2,773,924
  ghostd staking network weight  : 8,426,392

  ghostd staking currently?      : YES  (NO when no coins are delegated)
  ghostd staking wallet weight   : some amount (x.xxx%)
  ghostd coldstaking balance     : some amount

* Inbound P2P Port is not open - this is okay and will not affect the function of this staking node.
  However by opening port 51728/tcp you can provide full resources to the Ghost Network by acting as a 'full node'.
  A 'full staking node' will increase the number of other nodes you connect to beyond the 16 limit.
Exiting.

ghost@raspberrypi:~/ghostman/bin $
```

22. HowTo cold stake your coins in Wallet please look at VPS cold staking Paper
    * https://medium.com/@GhostbyMcAfee/vps-cold-staking-setup-612d6f63242b

### Autostart
to activate autostart of ghostd and Webserver:
edit crontab file with
```
crontab -e
```
past this 5 lines
```
@reboot      sleep 40  && bash /home/ghost/ghostman/bin/ghostman.sh restart now  >> /home/ghost/tmp/Gman_start.log 2>&1
@reboot      sleep 60  && cd /home/ghost/ghostman/webserver  && /bin/bash /home/ghost/ghostman/webserver/webserver restart  >> /home/ghost/tmp/Gman_WebStart.log 2>&1
10 0 * * *   cd /home/ghost/ghostman                         && /bin/bash /home/ghost/ghostman/bin/ghostman.sh update       >> /home/ghost/tmp/Gman_update.log 2>&1
*/5 * * * *  cd /home/ghost/ghostman/webserver               && /bin/bash /home/ghost/ghostman/webserver/scripts/cron.sh    >> /home/ghost/tmp/Gman_WebScript.log 2>&1
* */2 * * *  cd /home/ghost/ghostman/webserver               && /bin/bash /home/ghost/ghostman/webserver/webserver restart  >> /home/ghost/tmp/Gman_WebStart.log 2>&1
```
and save with CTRL-x,y,ENTER


reboot Rasbperry with
```
sudo reboot
```
Login again and check status with
```
bash /~/ghostman/bin/ghostman.sh status
```

### Update Ghostman
run Update with
```
bash /~/ghostman/bin/ghostman.sh update
```
this will not be necessary because crontab commands above will check for Updates every Day at 00:10

## ToDo
### backup
easiest way is to put SD-Card in PC make a full Image with a Tool like Win32 Disk Imager
https://sourceforge.net/projects/win32diskimager/




