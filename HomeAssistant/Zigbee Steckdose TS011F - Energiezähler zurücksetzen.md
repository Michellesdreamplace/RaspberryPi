## Home Assistant - Zigbee Steckdose TS011F - Energiezähler zurücksetzen



!! Stelle sicher, dass der Stecker eingeschaltet ist !!

Home Assistant

Kategorie: Einstellungen

Geräte und Dienste

Zigbee Home Automation

Powerplug (der Name, den ich dem TS011 gegeben habe)

- Geräte-Informationen – klicke auf die drei Punkte rechts neben „Neu konfigurieren“
- Zigbee-Gerät verwalten
  - auf den Reiter „Befehle“ klicken
  - unter „reset_fact_default (id: 0x0000)“ bei „Hersteller-Code überschreiben“ den Wert „1“ eingeben und dann unten „Zigbee-Befehl absetzen“ anklicken.

Aktualisiere die Seite, und der Wert für den Energieverbrauch steht wieder auf 0.
