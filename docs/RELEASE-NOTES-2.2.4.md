# Fabric Commander Linux Client 2.2.4

Dieses Release enthält die nativen Linux-Clients für AMD64/x86_64 und ARM64, jeweils mit GUI oder Headless.

## Installation und Updates

- Native, binäre TAR-Installer für die Erstinstallation; kein Git-Checkout und keine Python-Entwicklungsumgebung nötig.
- Vier getrennte RSA-signierte Update-ZIPs, jeweils an Architektur, Clientvariante und Versionsstand gebunden.
- Separat signierte Linux-OTA-Kanaldeskriptoren. Die Clientsoftware prüft Signaturen und SHA-256 vor einem Update, auch wenn das Gateway nicht erreichbar ist.
- Verwaltung als systemd-Benutzerdienst, Status- und Updatebefehle über die Linux-CLI; Administratoren können die globale `fclient`-Steuerung installieren.
- Für Headless-Geräte ist die Weboberfläche optional. Die Einrichtungsabfrage entscheidet vor dem Pairing, ob der Webdienst gestartet wird.
- Ein Rollback auf einen vorhandenen vorherigen Installationsslot ist vorgesehen.

**Wichtig:** Immer nur GUI oder Headless passend zur eigenen CPU laden. Die ZIP-Dateien sind Updatepakete; zur Neuinstallation die jeweilige TAR-Datei verwenden.

## Download und Sicherheit

Alle Downloads sind ausschließlich Binärartefakte oder die für ihre Überprüfung benötigten signierten Metadaten. Private Signierschlüssel und Quellcode werden nicht veröffentlicht.

[Dateien zu 2.2.4](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.4) · [SHA-256-Prüfsummen](SHA256-2.2.4.md)
