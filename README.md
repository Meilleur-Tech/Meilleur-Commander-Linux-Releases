# Fabric Commander Client · Linux

**Offizielle Linux-Downloads für Fabric Commander** | Official Linux client distributions.

[**Aktuelle Version herunterladen (Latest)**](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/latest) · [Release-Änderungen 2.2.4](docs/RELEASE-NOTES-2.2.4.md) · [Installation 2.2.4 (DE)](docs/INSTALLATION-2.2.4.md) · [Fehlerbehebung (DE)](docs/FEHLERBEHEBUNG.md) · [Prüfsummen & Sicherheit 2.2.4](docs/SICHERHEIT-2.2.4.md)

**Aktuelle Linux-Version: 2.2.4**, veröffentlicht für zwei CPU-Architekturen und zwei getrennte Clientvarianten. Native RSA-signierte Updates bleiben an die passende CPU-Architektur und GUI/Headless-Variante gebunden. Der unabhängige Linux-OTA-Kanal verifiziert zusätzliche signierte Kanaldeskriptoren und funktioniert bei einem ausgefallenen Gateway ohne eine Gateway-Freigabe. Das Linux-Release ist unabhängig von Gateway-, Windows- und macOS-Versionen.

## Welche Datei brauche ich?

Zuerst im **Linux-Terminal** prüfen:

```bash
uname -m
```

| System | Desktop mit GUI | Server ohne Desktop (Headless) |
|---|---|---|
| `x86_64` (AMD/Intel 64 Bit) | [GUI x86_64 2.2.4](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.4/Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.4.tar.gz) | [Headless x86_64 2.2.4](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.4/Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.4.tar.gz) |
| `aarch64` / `arm64` (ARM 64 Bit) | [GUI ARM64 2.2.4](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.4/Meilleur-Commander-Client-Linux-GUI-arm64-2.2.4.tar.gz) | [Headless ARM64 2.2.4](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.4/Meilleur-Commander-Client-Linux-HEADLESS-arm64-2.2.4.tar.gz) |

**Für die Neuinstallation die `.tar.gz`-Datei laden.** Die vier zusätzlich veröffentlichten `.zip`-Dateien sind die **architektur- und variantenabhängigen signierten Updatepakete**. Sie sind keine zweite Installationsmethode. Für 2.2.4 wird in diesem Release **kein .deb, .rpm, Synology-SPK oder QNAP-QPKG** bereitgestellt.

## In wenigen Minuten installieren

Keine Root-Installation, kein Git-Checkout und keine eigene Python-Umgebung nötig. Das passende Archiv herunterladen, dann im Terminal (hier Beispiel **x86_64 Headless**) ausführen:

```bash
cd ~/Downloads
tar -xzf Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.4.tar.gz
cd Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.4
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

Der Einrichtungsdialog fragt die **HTTPS-Gateway-Adresse** ab, zeigt einen Gerätecode und den Freigabelink. Die Kopplung wird im Browser bestätigt. Der Headless-Installer bietet zusätzlich eine **HTTPS-Webverwaltung im LAN** mit anfänglichem Administratorzugang und verpflichtendem Passwortwechsel. Zugangsdaten und einmaligen Aktivierungscode nur der lokalen Installationsausgabe entnehmen und nicht auf GitHub posten.

**Bestehende Installation?** Für den einmaligen Wechsel von 2.2.2/2.2.3 auf 2.2.4 ist das signierte vollständige TAR-Archiv erforderlich; die alten Clients kennen den neuen Linux-OTA-Kanal noch nicht. Danach funktionieren die unabhängigen signierten OTA-Updates, sobald der entsprechende öffentliche Kanal aktiv ist. Bei bereits auf 2.2.4 umgestellten Clients gilt: `commander-client update --check` und `commander-client update`. Bei einer Installation mit altem 2.2.1 zuerst `meilleur-client update` verwenden; der neue Name erscheint nach dem Upgrade automatisch. Pairing und gespeicherte Clientdaten bleiben erhalten.

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
- [SHA-256-Prüfsummen aller acht 2.2.4-Dateien](docs/SHA256-2.2.4.md)
- [Release 2.2.4 mit Änderungsübersicht](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.4)
- [Fehler/Verbesserungen melden](https://github.com/Meilleur-Tech/Meilleur-Commander/issues) (keine Tokens, Kennwörter oder Enrollment-Codes hochladen)

**Keine pauschale NAS-Freigabe:** Synology DSM und QNAP QTS/QuTS benötigen eigene SPK-/QPKG-, libc-, Dienst- und Geräteprüfungen; ARMv7/32-Bit wird nicht unterstützt. Ein ARM64-Prozessor allein beweist keine NAS-Kompatibilität. [NAS-Tracking #1668](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1668).

### Release-Vertrauensmodell

Dieses Repository enthält öffentliche **Binärartefakte und Dokumentation**, nicht die privaten Signaturschlüssel. Das GitHub-Label **Latest** zeigt die öffentlich angebotene Version, ist aber **kein Signatur- oder Vertrauensbeweis**. Der Linux-Client 2.2.4 verwendet vier eigenständige öffentliche Kanaldeskriptoren für x86_64/ARM64 und GUI/Headless. Vor einer Installation prüft er mit seinem fest hinterlegten RSA-Vertrauensschlüssel den signierten Kanaldeskriptor, das signierte Release-Manifest, die SHA-256-Prüfsumme, Architektur, Variante und zulässige Version. **Gateway und Pairing sind für diese öffentliche Updateprüfung keine Voraussetzung.** Ein Owner-/Kundengateway kann getrennt davon für verwaltete Geräte eine bereits veröffentlichte Version freigeben oder zurückstellen; es darf weder den Linux-Client bauen noch als zwingende Paketquelle dienen. Die vier Kanalzeiger müssen bei jeder Latest-Veröffentlichung gemeinsam und geprüft aktiviert sein.

**Hinweis zu Altmetadaten:** `channels/stable.json` beschreibt nur das historische **2.1.0-x86_64-GUI-Einzelformat**. Für 2.2.4 gelten stattdessen die vier separat RSA-signierten öffentlichen Linux-Kanäle. Bei Bestandsinstallationen 2.2.2/2.2.3 ist der einmalige signierte Installer-Übergang nötig, da deren alter Updater noch den bisherigen Gateway-Kanal verwendet. Details stehen in der [aktuellen Sicherheitsbeschreibung](docs/SICHERHEIT-2.2.4.md).

Öffentliche Signaturidentität für Releaseprüfungen: RSA-Key-ID `mc-client-caf94007b07dc90b`. Dieses Repository enthält keine privaten Entwicklungsdateien oder Signierschlüssel.

---

**English quick start:** Choose the native `GUI` or `HEADLESS` **.tar.gz** matching `uname -m`; extract, enter the extracted directory and run `./install.sh` as a normal user. Run `commander-client setup` to connect an HTTPS Gateway and approve device pairing in a browser. Use `commander-client status`, `commander-client update --check` and `commander-client update`. The legacy `meilleur-client` alias remains valid. Signed ZIPs are for managed updates, not manual first installation. Synology/QNAP are not certified. See the detailed German installation and troubleshooting guides above.
