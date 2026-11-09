# Fabric Commander Client · Linux

**Offizielle Linux-Downloads für Fabric Commander** | Official Linux client distributions.

[**Aktuelle Version herunterladen (Latest)**](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/latest) · [Release-Änderungen 2.2.5](docs/RELEASE-NOTES-2.2.5.md) · [Installation 2.2.5 (DE)](docs/INSTALLATION-2.2.5.md) · [Fehlerbehebung (DE)](docs/FEHLERBEHEBUNG.md) · [Prüfsummen & Sicherheit 2.2.5](docs/SICHERHEIT-2.2.5.md)

**Vorbereiteter Linux-Release 2.2.5**, verfügbar nach signierter Freigabe für zwei CPU-Architekturen und zwei getrennte Clientvarianten. Native RSA-signierte Updates bleiben an die passende CPU-Architektur und GUI/Headless-Variante gebunden. Der unabhängige Linux-OTA-Kanal verifiziert zusätzliche signierte Kanaldeskriptoren und funktioniert bei einem ausgefallenen Gateway ohne eine Gateway-Freigabe. Das Linux-Release ist unabhängig von Gateway-, Windows- und macOS-Versionen.

## Welche Datei brauche ich?

Zuerst im **Linux-Terminal** prüfen:

```bash
uname -m
```

| System | Desktop mit GUI | Server ohne Desktop (Headless) |
|---|---|---|
| `x86_64` (AMD/Intel 64 Bit) | [GUI x86_64 2.2.5](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.5/Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.5.tar.gz) | [Headless x86_64 2.2.5](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.5/Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.5.tar.gz) |
| `aarch64` / `arm64` (ARM 64 Bit) | [GUI ARM64 2.2.5](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.5/Meilleur-Commander-Client-Linux-GUI-arm64-2.2.5.tar.gz) | [Headless ARM64 2.2.5](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.5/Meilleur-Commander-Client-Linux-HEADLESS-arm64-2.2.5.tar.gz) |

**Für die Neuinstallation die `.tar.gz`-Datei laden.** Die vier zusätzlich veröffentlichten `.zip`-Dateien sind die **architektur- und variantenabhängigen signierten Updatepakete**. Sie sind keine zweite Installationsmethode. Für 2.2.5 wird in diesem Release **kein .deb, .rpm, Synology-SPK oder QNAP-QPKG** bereitgestellt.

## In wenigen Minuten installieren

Keine Root-Installation, kein Git-Checkout und keine eigene Python-Umgebung nötig. Das passende Archiv herunterladen, dann im Terminal (hier Beispiel **x86_64 Headless**) ausführen:

```bash
cd ~/Downloads
tar -xzf Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.5.tar.gz
cd Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.5
./install.sh
```

Für die GUI stattdessen das **GUI-Archiv** der passenden CPU entpacken:

```bash
./install.sh --background on --tray on
```

Die Befehle `commander-client` und der ältere kompatible Alias `meilleur-client` stehen nach der Installation zur Verfügung. In bereits offenen Shells einmal `source ~/.bashrc` ausführen oder `~/.local/bin/commander-client` verwenden.

```bash
commander-client setup
commander-client status
commander-client update --check
```

**Hosted CTRL Headless:** Im Linux-Terminal commander-client account connect starten. Die angezeigte Bestätigungsadresse samt einmaligem Code auf einem anderen Rechner oder Smartphone im Browser öffnen, beim Kundenkonto bestätigen und die Rückmeldung im Terminal abwarten. Auf dem Linux-Server ist dafür kein lokaler Browser nötig. **Privates Gateway:** Mit commander-client setup bleibt die bestehende direkte Gateway-Kopplung verfügbar. Der Headless-Installer bietet zusätzlich eine **HTTPS-Webverwaltung im LAN** mit anfänglichem Administratorzugang und verpflichtendem Passwortwechsel. Zugangsdaten und einmaligen Aktivierungscode nur der lokalen Installationsausgabe entnehmen und nicht auf GitHub posten.

**Bestehende Installation?** Von Linux 2.2.4 auf 2.2.5 erfolgt das signierte Update über den bisherigen kompatiblen, signierten 2.2.4-Kanal und anschließend den unabhängigen GitHub-Latest-Kanal. Befehl: commander-client update --check, danach commander-client update. Ältere 2.2.2/2.2.3-Geräte benötigen zuerst ein vollständiges signiertes TAR-Upgrade, weil sie keinen eigenständigen Linux-OTA-Kanal besitzen. Kopplung und lokale Clientdaten bleiben erhalten; Rollback verwendet einen vorhandenen alten Slot.

## Die wichtigsten Befehle

| Befehl | Funktion |
|---|---|
| `commander-client setup` | Gateway und Gerätefreigabe einrichten |
| `commander-client status` | Gut lesbarer Verbindungsstatus |
| `commander-client status --json` | Maschinenlesbare Diagnose |
| `commander-client update --check` | Signierte Updates prüfen, als Terminalübersicht |
| `commander-client update --check --json` | Maschinenlesbare Updateprüfung |
| `commander-client update` | Zugewiesenes, signiertes Update installieren |
| `commander-client update --json` | Update mit JSON-Ausgabe, auch im Terminal |
| `commander-client rollback` | Vorherige installierte Version wiederherstellen, sofern vorhanden |
| `commander-client web status` | Headless-WebUI-Adresse und Status anzeigen |
| `commander-client web password reset` | Lokalen Headless-WebUI-Zugang zurücksetzen |
| `commander-client logs` | Client-Ereignisse anzeigen |
| `commander-client uninstall` | Programm entfernen, lokale Kopplungsdaten behalten |
| `commander-client uninstall --purge` | Auch lokale Kopplungs-/Zugangsdaten entfernen |

Die interaktive Linux-CLI zeigt Status, Updateprüfung, Update und Rollback als lesbare Textbox. Umgeleitete Aufrufe behalten die JSON-Ausgabe für Skripte und WebUI. Interne Datenverzeichnisse und systemd-Dienstnamen verwenden **aus Kompatibilitätsgründen weiterhin** `meilleur-client`.

## Support & Sicherheit

- [Installation und x64-Testablauf (DE)](docs/INSTALLATION.md)
- [Häufige Probleme und Lösungen (DE)](docs/FEHLERBEHEBUNG.md)
- [SHA-256-Prüfsummen aller acht 2.2.5-Dateien](docs/SHA256SUMS-2.2.5.txt)
- [Release 2.2.5 mit Änderungsübersicht](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.5)
- [Fehler/Verbesserungen melden](https://github.com/Meilleur-Tech/Meilleur-Commander/issues) (keine Tokens, Kennwörter oder Enrollment-Codes hochladen)

**Keine pauschale NAS-Freigabe:** Synology DSM und QNAP QTS/QuTS benötigen eigene SPK-/QPKG-, libc-, Dienst- und Geräteprüfungen; ARMv7/32-Bit wird nicht unterstützt. Ein ARM64-Prozessor allein beweist keine NAS-Kompatibilität. [NAS-Tracking #1668](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1668).

### Release-Vertrauensmodell

Dieses Repository enthält öffentliche **Binärartefakte und Dokumentation**, nicht die privaten Signaturschlüssel. Das GitHub-Label **Latest** zeigt die öffentlich angebotene Version, ist aber **kein Signatur- oder Vertrauensbeweis**. Der Linux-Client 2.2.5 verwendet vier eigenständige öffentliche Kanaldeskriptoren für x86_64/ARM64 und GUI/Headless. Vor einer Installation prüft er mit seinem fest hinterlegten RSA-Vertrauensschlüssel den signierten Kanaldeskriptor, das signierte Release-Manifest, die SHA-256-Prüfsumme, Architektur, Variante und zulässige Version. **Gateway und Pairing sind für diese öffentliche Updateprüfung keine Voraussetzung.** Ein Owner-/Kundengateway kann getrennt davon für verwaltete Geräte eine bereits veröffentlichte Version freigeben oder zurückstellen; es darf weder den Linux-Client bauen noch als zwingende Paketquelle dienen. Die vier Kanalzeiger müssen bei jeder Latest-Veröffentlichung gemeinsam und geprüft aktiviert sein.

**Hinweis zu Altmetadaten:** `channels/stable.json` beschreibt nur das historische **2.1.0-x86_64-GUI-Einzelformat**. Für 2.2.5 gelten stattdessen die vier separat RSA-signierten öffentlichen Linux-Kanäle. Bei Bestandsinstallationen 2.2.2/2.2.3 ist der einmalige signierte Installer-Übergang nötig, da deren alter Updater noch den bisherigen Gateway-Kanal verwendet. Details stehen in der [aktuellen Sicherheitsbeschreibung](docs/SICHERHEIT-2.2.5.md).

Öffentliche Signaturidentität für Releaseprüfungen: RSA-Key-ID `mc-client-caf94007b07dc90b`. Dieses Repository enthält keine privaten Entwicklungsdateien oder Signierschlüssel.

---

**English quick start:** Choose the native `GUI` or `HEADLESS` **.tar.gz** matching `uname -m`; extract, enter the extracted directory and run `./install.sh` as a normal user. Run `commander-client setup` to connect an HTTPS Gateway and approve device pairing in a browser. Use `commander-client status`, `commander-client update --check` and `commander-client update`. The legacy `meilleur-client` alias remains valid. Signed ZIPs are for managed updates, not manual first installation. Synology/QNAP are not certified. See the detailed German installation and troubleshooting guides above.
