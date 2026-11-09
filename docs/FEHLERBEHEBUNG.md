# Fabric Commander Linux 2.2.5 · Fehlerbehebung

[Downloads](../README.md) | [Installation](INSTALLATION.md) | [Sicherheit](SICHERHEIT-UND-KOMPATIBILITAET.md)

## Headless-Hosted-Anmeldung: account_browser_unavailable

Version des installierten Clients mit commander-client status prüfen. Die alte öffentliche 2.2.4 unterstützt die Hosted-Kontoanmeldung auf einem Linux-Gerät ohne lokalen Browser nicht vollständig. Der korrigierte 2.2.5-Client stellt für die Hosted-Anbindung commander-client account connect bereit: Code und Bestätigungsadresse am Linux-Server anzeigen, auf einem zweiten Gerät im Browser anmelden und die Freigabe bestätigen. Der Linux-Server selbst benötigt keinen Desktop. Private Gateway-Kopplung ist ein anderer Weg und verwendet weiterhin commander-client setup.

## Updatequelle nicht erreichbar

Mit commander-client update --check die signierte Linux-Version prüfen. Ein neuer GitHub Latest stellt nur dann Updates bereit, wenn der vollständige architektur-/variantenrichtige RSA-signierte Kanal, Manifest und Paket-SHA256 vorhanden sind. Für schon installierte 2.2.4-Clients wird der bisherige signierte Legacy-Kanal bei der Veröffentlichung automatisch mitgeführt. Fehlt GitHub-Konnektivität oder stimmt ein Hash nicht, darf kein erzwungenes unsigniertes Ersatzpaket verwendet werden.

## Dienst oder Befehl nicht verfügbar

Bei nicht gefundenem commander-client eine neue Shell öffnen und ~/.local/bin/commander-client status versuchen. Den systemd-User-Dienst als ursprünglich installierenden Benutzer prüfen. Keine Benutzerdateien, Kopplungsdaten oder Credentials manuell entfernen. Bei Updatefehlern commander-client rollback verwenden, sofern ein alter Installationsslot existiert. GUI benötigt eine passende Desktoplaufzeit; Headless benötigt keine Desktopbibliotheken.
