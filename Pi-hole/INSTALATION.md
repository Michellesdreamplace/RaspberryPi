# 🔧 Komplette Neuinstallation von Pi-hole auf Raspberry Pi 

##📋 Vorbereitung: Alte Installation komplett entfernen

### 1. System aktualisieren
```
sudo apt update && sudo apt full-upgrade -y
sudo apt autoremove -y
sudo apt clean
```

### 2. Pi-hole komplett deinstallieren
```
# Pi-hole deinstallieren
pihole uninstall

# Alle verbleibenden Dateien entfernen
sudo rm -rf /etc/pihole/
sudo rm -rf /opt/pihole/
sudo rm -rf /var/www/html/admin/
sudo rm -f /etc/dnsmasq.d/01-pihole.conf
sudo rm -f /etc/dnsmasq.d/02-pihole-dhcp.conf
sudo rm -f /etc/cron.d/pihole
```

### 3. Abhängigkeiten installieren
```
sudo apt install curl git dnsutils lighttpd php-common php-cgi sqlite3 -y
```

## 🚀 Pi-hole Neuinstallation

### 4. Offizielles Installationsscript ausführen
```
# Pi-hole mit automatischer Installation
curl -sSL https://install.pi-hole.net | bash
```

Wichtige Einstellungen während der Installation:
- Upstream DNS: Cloudflare (1.1.1.1 und 1.0.0.1) oder nach Preference
- Blocklists: Standardlisten aktivieren
- Web Interface: Ja aktivieren
- Web Server: lighttpd aktivieren
- Logging: Ja aktivieren
- Query Logging: Aktivieren für Debugging

### 5. Alternativ: Interaktive Installation
```
# Für mehr Kontrolle über den Installationsprozess
git clone --depth=1 https://github.com/pi-hole/pi-hole.git Pi-hole
cd "Pi-hole/automated install/"
sudo bash basic-install.sh
```

## ⚙️ Konfiguration nach der Installation

### 6. Web Interface Passwort setzen
```
pihole -a -p
```


