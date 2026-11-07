# Fabric Commander Linux 2.2.4 installieren und aktualisieren

## Neuinstallation

Im Terminal zuerst die Architektur ermitteln:

```bash
uname -m
```

Für `x86_64` die x86_64-Datei verwenden, für `aarch64` die ARM64-Datei. **Headless** ist für Server ohne Desktop, **GUI** für Linux-Desktops.

[Linux 2.2.4 herunterladen](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.4)

Beispiel für einen x86_64-Server, als **normaler Linux-Benutzer**:

```bash
cd ~/Downloads
tar -xzf Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.4.tar.gz
cd Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.4
./install.sh
```

Beim ersten interaktiven Setup fragt der Installer **vor dem Pairing**, ob der lokale HTTPS-Webserver eingerichtet und als Benutzerdienst gestartet werden soll. **J/Y** ist die Standardantwort, **N** deaktiviert den Webserver. Für einen strikt nichtinteraktiven Headless-Server ohne Webserver und Hintergrunddienst:

```bash
./install.sh --non-interactive --web off --background off --tray off
```

Anschließend:

```bash
~/.local/bin/commander-client setup
~/.local/bin/commander-client status
~/.local/bin/fclient status
```

Die Kopplung mit dem Gateway geschieht über den angezeigten Gerätecode und die Freigabe im Browser. Ein fehlender Gatewayzugriff ist keine Erlaubnis, unsignierte Updates zu installieren.

## Bestehende Installationen 2.2.2 oder 2.2.3

**Einmaliger Übergang:** Der alte Linux-Client zeigt bei `update --check` möglicherweise nur 2.2.2 oder 2.2.3 als aktuell an. Das ist der bisherige Gateway-Kanal, nicht der neue eigenständige Linux-OTA-Kanal. Die neue Kanal-Erkennung ist erst ab 2.2.4 im installierten Client enthalten. Deshalb 2.2.4 zunächst mit dem **signierten vollständigen TAR-Installer** der passenden Architektur/Variante über die vorhandene Installation installieren. Danach die bestehende Kopplung, WebUI-Einstellungen, Dienste und den vorherigen Rollback-Slot prüfen.

**Legacy-Dateirechte:** Bei einem getesteten 2.2.2-Headless-Gerät war `~/.local/share/meilleur-client` mit Modus `0775` gruppenbeschreibbar. Die strengere 2.2.4-Metadatenprüfung beendet die Installation zu Recht mit `unsafe user metadata parent`. Wenn genau dieses Problem auftritt, als bisheriger Client-Benutzer zunächst prüfen, dass das Verzeichnis keine symbolische Verknüpfung ist und dem eigenen Benutzer gehört. Dann **nur das betroffene Verzeichnis** sichern und die Gruppen-Schreibberechtigung entfernen:

```bash
dir="$HOME/.local/share/meilleur-client"
test -d "$dir" && test ! -L "$dir" && test -O "$dir" && chmod g-w "$dir"
```

Nicht rekursiv umberechtigen, keine Root-Installation und keinen Sicherheitscheck deaktivieren. Vor dem einmaligen Upgrade einen VM-Snapshot oder eine überprüfte Datensicherung erstellen. Die RSA-signierten Installer-Metadaten und Hashes sind vor der Installation zu überprüfen.

## Update und Rollback

```bash
~/.local/bin/commander-client update --check
~/.local/bin/commander-client update
~/.local/bin/fclient status
~/.local/bin/fclient rollback
```

Der unabhängige Linux-OTA-Kanal verifiziert einen separat RSA-signierten Kanaldeskriptor, das signierte Release-Manifest sowie die SHA-256-Prüfsumme. Es gibt getrennte Kanäle für x86_64/ARM64 und GUI/Headless. Für den Fall einer fehlenden früheren Installation steht kein Rollback-Slot zur Verfügung.

## Sicherheit

Die vollständigen TAR-Installer sind für Neuinstallationen vorgesehen. ZIP-Dateien dienen ausschließlich als signierte Updates. Nur Dateien verwenden, die exakt zur CPU-Architektur und GUI-/Headless-Variante passen. Die [SHA-256-Prüfsummen](SHA256-2.2.4.md) erlauben eine unabhängige Integritätsprüfung. Private Schlüssel, Pairing-Codes und Passwörter nicht in Issues veröffentlichen.
