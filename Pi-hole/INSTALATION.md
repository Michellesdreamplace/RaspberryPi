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

### 7. Wichtige Konfigurationen prüfen
```
# Prüfen ob alle Dateien erstellt wurden
ls -la /etc/pihole/
ls -la /etc/dnsmasq.d/

# Gravity Liste sollte gefüllt sein
ls -la /etc/pihole/gravity.list
head -n 5 /etc/pihole/gravity.list
```

### 8. Blocklisten hinzufügen
```
# Zur Web-Oberfläche gehen: http://pi.hole/admin
# Oder über SSH: 
# pihole -g (Update der Gravity-Datenbank)
```

## 🔧 Netzwerkkonfiguration

### 9. Statische IP für Raspberry Pi setzen
```
# Aktuelle IP ermitteln
hostname -I

# Statische IP konfigurieren (Beispiel)
sudo nano /etc/dhcpcd.conf
```
Folgende Zeilen hinzufügen (an Ihre Netzwerkkonfiguration anpassen):
```
interface eth0
static ip_address=192.168.178.100/24
static routers=192.168.178.1
static domain_name_servers=192.168.178.1
```

### 10. FritzBox konfigurieren
- FritzBox Oberfläche öffnen (http://fritz.box)
- Internet → Filter → Listen
- DNS-Server auf die IP Ihres Raspberry Pi setzen
- Änderungen speichern

## ✅ Funktionstest

### 11. Pi-hole Status prüfen
```
pihole status
pihole version
```

### 12. DNS Funktionalität testen
```
# Test mit lokalem DNS
dig @127.0.0.1 google.com +short

# Blocking testen
dig @127.0.0.1 doubleclick.net +short
# Sollte "0.0.0.0" zurückgeben

# Externer Test
dig @1.1.1.1 google.com +short
```

### 13. Web Interface testen
```
# Web Interface aufrufen
echo "Pi-hole Web Interface: http://$(hostname -I | awk '{print $1}')/admin"
```

## 🛠 Problembehandlung

### 14. Falls Probleme auftreten
```
# Debug-Modus
pihole -d

# Logs anzeigen
pihole tail

# Gravity update erzwingen
pihole -g

# DNS neu starten
pihole restartdns
```

### 15. Wichtige Dateien prüfen
```
# Prüfen ob Konfiguration existiert
sudo ls -la /etc/dnsmasq.d/*pihole*

# Hosts-Dateien prüfen
sudo ls -la /etc/pihole/*.list
sudo head -n 10 /etc/pihole/gravity.list

# DNSMASQ Konfiguration testen
dnsmasq --test
```

## 🔒 Sicherheitseinstellungen

### 16. Firewall konfigurieren
```
# UFW Firewall installieren und konfigurieren
sudo apt install ufw
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow domain
sudo ufw enable
```

### 17. Regelmäßige Updates
```
# Automatische Updates einrichten
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades
```

## 📊 Monitoring und Wartung

### 18. Überwachung einrichten
```
# Pi-hole eigene Statistik
pihole -c

# Externes Monitoring (optional)
# sudo apt install prometheus-node-exporter
```

### 19. Regelmäßige Wartung
```
# Cron-Job für automatische Updates
sudo crontab -l | grep pihole

# Manuell updaten
pihole -up
```

## 💡 Wichtige Hinweise

1. Notieren Sie das Web Interface Passwort
2. Testen Sie die Konfiguration bevor Sie alle Geräte umstellen
3. Erstellen Sie Backups der Konfiguration
4. Überwachen Sie die Logs in den ersten Tagen

Zugangsdaten:
- Web Interface: http://[Ihre-Raspberry-Pi-IP]/admin
- SSH: Wie gewohnt mit Ihrem Benutzer

Bei Problemen:
- Debug-Modus: pihole -d
- Logs: pihole tail
- Forum: https://discourse.pi-hole.net/

