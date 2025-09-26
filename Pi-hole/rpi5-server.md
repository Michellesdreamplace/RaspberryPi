
> ###### Welche Firmwareversion habe ich?

```
uname -a
```

> ###### Beispiel-Antwort:
```
Linux rpi5 6.12.47+rpt-rpi-2712 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1~bookworm (2025-09-16) aarch64 GNU/Linux
```

> ##### Das Update
> ###### Für das Firmwareupdate benutzten wir Hexxeh's praktisches Updateskript das uns die aktuellste Firmware herunterlädt und installiert. <br/>
<br/>
<br/>
<br/>
<br/>

> ###### Bevor wir das starten können muss zunächst einmal Git nachinstalliert werden.
```
sudo apt-get update
sudo apt-get install git
```

> ###### Nun laden wir das Skript herunter und setzen gleich die Ausführungsrechte.
```
sudo wget https://raw.github.com/Hexxeh/rpi-update/master/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
# oder:
sudo wget https://raw.githubusercontent.com/Michellesdreamplace/RaspberryPi/refs/heads/main/Pi-hole/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
```

> ###### Zum Schluss starten wir den Aktualisierungsvorgang indem wir das Skript starten.
```
sudo rpi-update
```

> ###### Nachdem das Skript fertig ist müsst ihr nur noch das System neustarten.
```
sudo reboot
```

> ###### Nochmals die Firmwareversion prüfen:
```
uname -a
```

> ###### Beispiel-Antwort:
```
Linux rpi5 6.12.48-v8-16k+ #1905 SMP PREEMPT Mon Sep 22 13:35:50 BST 2025 aarch64 GNU/Linux
```














sudo apt-get update
sudo apt-get upgrade


sudo apt update
sudo apt full-upgrade -y
sudo rpi-update




sudo raspi-config

sudo apt-get install xrdp

