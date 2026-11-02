# Installation und Betrieb · Meilleur Commander Linux 2.2.2

[← README](../README.md) · [Aktueller Release](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/latest) · [Fehlerbehebung](FEHLERBEHEBUNG.md)

## Voraussetzungen

- Linux mit **x86_64** (Intel/AMD 64 Bit) oder **aarch64/arm64** (ARM 64 Bit).
- Ein normaler Linux-Benutzer mit eigenem Home-Verzeichnis und Schreibrechten in `~/.local`; **nicht** als `root` oder mit `sudo ./install.sh` installieren.
- Für GUI: funktionierende Desktop-/Grafikumgebung (z. B. GNOME/KDE) mit erforderlichen Display-, Grafik-, Font- und D-Bus-Bibliotheken.
- Für Headless: keine Qt- oder Desktop-Bibliotheken nötig; für den dauerhaften Hintergrundbetrieb ist ein **systemd-User-Dienst** vorgesehen. Ein Server ohne passenden systemd-Benutzerdienst ist nicht automatisch freigegeben.
- Erreichbarer HTTPS-Gateway mit aktivem Geräte-Pairing und für deine Plattform passendem signiertem Updatekanal. Bei einer privaten CA muss deren Fingerabdruck vorher durch den Administrator geprüft und das Systemvertrauen korrekt eingerichtet sein.
- Für die Headless-LAN-WebUI einen privaten IP-Zugang und einen Browser, mit dem das lokale TLS-Zertifikat anhand seines ausgegebenen SHA-256-Fingerabdrucks geprüft werden kann.

Architektur:

```bash
uname -m
```

`x86_64` → x86_64-Archiv; `aarch64`/`arm64` → arm64-Archiv. Eine Rosetta-VM auf Apple Silicon läuft normalerweise als ARM64-Gast: nicht automatisch das x86_64-Archiv wählen.

## Neue Installation

### Variante A: x86_64 Headless (Server, Chris' Testfall)

1. Im [Release 2.2.2](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.2) die Datei `Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2.tar.gz` herunterladen.
2. SHA-256 gegen die [offizielle Dateiliste](SHA256SUMS-2.2.2.txt) prüfen.
3. Als normaler Benutzer:

```bash
cd ~/Downloads
sha256sum Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2.tar.gz
tar -xzf Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2.tar.gz
cd Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2
./install.sh
```

Der Installer enthält den nativen Core, die Headless-WebUI, die geprüften Client-Vertrauensdaten und ein dauerhaftes Deinstallationsskript. Er braucht keine zusätzliche Python-Paketinstallation.

Anschließend ein **neues Terminal** öffnen (in einer alten Bash-Sitzung alternativ `source ~/.bashrc`) und ausführen:

```bash
commander-client setup
commander-client status
commander-client web status
```

Der Setup-Dialog fragt die Gateway-HTTPS-Adresse ab. Nach Anforderung des Gerätecodes den angezeigten Freigabelink im Browser öffnen und die Kopplung dort bestätigen. Das Gerät ist erst fertig eingerichtet, wenn `commander-client status` die bestätigte Verbindung zeigt. Die WebUI gibt ihre LAN-HTTPS-Adresse, den TLS-Zertifikatsfingerabdruck und den initialen Zugang beim lokalen Setup aus. Beim ersten Weblogin den einmaligen Aktivierungscode und danach ein eigenes Passwort verwenden.

**Sicherheitsregel:** WebUI-Zugang, Aktivierungscode und Zertifikatsfingerabdruck niemals in öffentliche Issues oder Screenshots mit Geheimnissen übernehmen.

### Variante B: x86_64 GUI (Desktop, Chris' Testfall)

Die Datei `Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.2.tar.gz` laden und prüfen. Dann:

```bash
cd ~/Downloads
tar -xzf Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.2.tar.gz
cd Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.2
./install.sh --background on --tray on
commander-client status
~/.local/bin/meilleur-commander-client
```

Der grafische Launcher heißt weiterhin `meilleur-commander-client`; **der neue allgemeine CLI-Befehl heißt `commander-client`**. Fehlt ein kompatibler GNOME-AppIndicator/KStatusNotifier, startet die Anwendung sichtbar statt unsichtbar im Tray zu verschwinden. Für GNOME/Wayland ggf. die AppIndicator-Erweiterung einschalten und neu anmelden. GUI und Headless nicht unter derselben lokalen Client-Identität parallel gegen unterschiedliche Gateways betreiben; bei getrennten Testzielen unterschiedliche Linux-Benutzer verwenden.

### ARM64

Genau dieselben Schritte, aber jeweils `arm64` im Archivnamen verwenden und die CPU vorher mit `uname -m` bestätigen. Die nativen ARM64- und x86_64-Ausgaben sind **unterschiedliche** Binaries; keine Dateien umbenennen oder über Rosetta „passend“ machen.

## Bestehenden Client aktualisieren

Ein vorhandener 2.2.1-Client darf **ohne neue Installation** über seinen vom Gateway zugewiesenen, signierten Kanal aktualisiert werden:

```bash
# Auf 2.2.1 den bestehenden Alias verwenden:
meilleur-client update --check
meilleur-client update

# Danach, ab 2.2.2:
commander-client status
commander-client update --check
commander-client update --check --json
```

Damit bleibt die vorhandene Geräte-ID und Kopplung erhalten. Der neue Launcher `commander-client` wird bei einem regulären Start/Statusaufruf des aktualisierten Cores automatisch ergänzt, ohne einen Installer ein zweites Mal auszuführen. Bestehende persönliche Dateien/Symlinks werden dafür nicht überschrieben. Der frühere Befehl `meilleur-client` bleibt kompatibel.

Ein Update wird **nur angeboten**, wenn das Gateway der richtigen Architektur und GUI-/Headless-Variante ein authentifiziertes, kompatibles Manifest zuweist. Das GitHub-Label `Latest` schaltet kein Gateway automatisch um.

### Rollback

Falls die zuvor installierte Version noch vorhanden ist:

```bash
commander-client rollback
commander-client status
```

Wenn zurück auf einen Stand vor 2.2.2 gewechselt wird, kann der alte Befehl `meilleur-client` als sichere Alternative weiterverwendet werden.

### JSON für Skripte

```bash
commander-client status --json
commander-client update --check --json
commander-client update --json
```

Interaktive Terminals zeigen eine lesbare Statusbox; umgeleitete Standardausgaben sind weiterhin maschinenlesbar. Beim Verarbeiten in Automationen dennoch Fehlercode und Felder prüfen.

## Hintergrunddienst und WebUI

```bash
commander-client web status
commander-client web on
commander-client web off
commander-client web port set 8999
commander-client web bind set lan
commander-client web bind set local
commander-client web password reset
```

Die WebUI läuft über **HTTPS im lokalen Netz**. Keine pauschale Internet-Portweiterleitung aktivieren. Bei Zertifikatswarnungen zuerst die Fingerabdruck-Identität aus der lokalen Installations-/Statusausgabe prüfen. Die Bridge und der Headless-Webserver können unabhängig verwaltet werden. Der Installer richtet passende Dienste im **Benutzerkontext** ein; die systemd-Units behalten aus Kompatibilitätsgründen den Präfix `meilleur-client`.

Wenn `systemctl --user` aus einer administrativen Fremdsitzung keine User-Bus-Verbindung findet, ist das **kein** Grund, den Client als root neu zu installieren. Stattdessen eine reguläre Login-Sitzung des Client-Benutzers verwenden und dessen User-Dienst überprüfen.

## Deinstallation

Für diese `.tar.gz`-Installation:

```bash
commander-client uninstall
# Nur wenn wirklich auch Kopplung, Konfiguration und geheime Clientdaten gelöscht werden sollen:
commander-client uninstall --purge
```

Ohne `--purge` bleiben die lokalen Benutzer-/Kopplungsdaten erhalten. Nach einer `--purge`-Entfernung ist eine erneute Gerätefreigabe erforderlich. Nicht mit älteren separaten `.deb`-Preview-Installationen verwechseln: Die hier beschriebenen **2.2.2-Assets sind TAR.GZ und signierte Update-ZIPs, keine .deb-Dateien**.

## Abnahmeprotokoll für Chris

Bei der ersten x86_64-Abnahme am besten diese Ergebnisse notieren, ohne Geheimnisse weiterzugeben:

1. `uname -m` und Linux-Distribution/Version; welche **GUI-/Headless**-Variante wurde verwendet?
2. SHA-256 der heruntergeladenen TAR.GZ-Datei gegen die Release-Prüfsummen.
3. Installation **ohne sudo** erfolgreich; `command -v commander-client` sowie `commander-client status` funktionieren.
4. Gateway/Pairing erfolgreich; Verbindungsanzeige bleibt auf **verbunden**.
5. Headless: HTTPS-WebUI, Passwortwechsel, Gateway-Auswahl und WebUI-Updateprüfung testen. GUI: sichtbares Fenster, Tray-Fallback und Updatefunktion.
6. `commander-client update --check` zeigt die neue Terminalübersicht; `--json` liefert gültiges JSON.
7. Falls eine ältere signierte Version als Ausgangspunkt vorhanden ist: 2.2.1 → 2.2.2 und Rollback prüfen; Geräteidentität vor/nach Update gleich.
8. Fehlersuche ohne vertrauliche Daten über [Fehlerbehebung](FEHLERBEHEBUNG.md), danach reproduzierbaren Befund im [Commander-Issue-Tracker](https://github.com/Meilleur-Tech/Meilleur-Commander/issues) dokumentieren.

**Abnahmestand:** ARM64 Headless 2.2.1 → 2.2.2 → 2.2.1 mit erhaltener Verbindung/Pairing erfolgreich getestet. Ein breiter, unabhängiger x86_64-GUI-/Headless-Endkundentest und NAS-Pakete werden damit **nicht** behauptet.
