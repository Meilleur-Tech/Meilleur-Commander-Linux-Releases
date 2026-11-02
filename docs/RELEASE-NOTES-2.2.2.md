# Meilleur Commander Client Linux 2.2.2

**Stable · Latest · 2 November 2026** · ARM64/AArch64 and x86_64 · GUI + Headless

Linux 2.2.2 is the first common release with the **`commander-client`** command, a readable terminal update status and a backwards-compatible upgrade path from `meilleur-client`. All four native Linux variants have independent RSA-signed update identities.

## Was ist neu? / What's new?

- **Neuer CLI-Name:** `commander-client` ist der bevorzugte Befehl; `meilleur-client` bleibt aus Kompatibilitätsgründen erhalten.
- **Terminal-Ansicht statt JSON-Salat:** `commander-client update --check`, `update` und `rollback` zeigen im interaktiven Linux-Terminal übersichtliche Statuskarten. Mit `--json` bzw. bei Umleitung bleibt die maschinenlesbare JSON-Ausgabe erhalten.
- **Sicheres In-Place-Upgrade:** Der neue Alias wird beim ersten regulären Start/Status nach einer signierten Aktualisierung ergänzt, **ohne Neuinstallation, Tokenverlust oder Re-Pairing**. Vorhandene State-/Systemd-Pfade bleiben unverändert.
- **Echte getrennte native Varianten:** GUI mit Desktop-Oberfläche oder Headless ohne Qt und ohne erforderlichen Desktop, jeweils für ARM64 und x86_64.
- **Headless-LAN-Verwaltung:** HTTPS-WebUI mit Login, verpflichtendem Passwortwechsel, Geräte-Pairing, Status und signierten Update-/Rollback-Aktionen. Die Adresse samt Zertifikatsfingerabdruck zeigt die lokale Einrichtung.
- **Sicherheit:** RSA-signierte Releases, architektur-/variantenfeste Manifeste, Paket-Hashprüfung und Gateway-Kompatibilität; ein generischer GitHub-Download umgeht diese Prüfungen nicht.

## Download / Which file?

**Neuinstallation: das TAR.GZ der passenden Architektur herunterladen.**

| Linux-CPU (`uname -m`) | GUI (Desktop) | Headless (Server/VM) |
|---|---|---|
| `x86_64` | [GUI x86_64 TAR.GZ](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.2/Meilleur-Commander-Client-Linux-GUI-x86_64-2.2.2.tar.gz) | [Headless x86_64 TAR.GZ](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.2/Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2.tar.gz) |
| `aarch64` / `arm64` | [GUI ARM64 TAR.GZ](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.2/Meilleur-Commander-Client-Linux-GUI-arm64-2.2.2.tar.gz) | [Headless ARM64 TAR.GZ](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/download/linux-client-v2.2.2/Meilleur-Commander-Client-Linux-HEADLESS-arm64-2.2.2.tar.gz) |

Die **vier zusätzlich gelisteten ZIP-Dateien** sind signierte GUI-/Headless-Updatepakete, **keine Installationsarchive für den Erststart**. Alle **acht** SHA-256-Dateihashes sind unter [Prüfsummen (2.2.2)](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/blob/main/docs/SHA256SUMS-2.2.2.txt) dokumentiert.

### Neuinstallation in der Shell

Beispiel **x86_64 Headless** (ohne `sudo`):

```bash
uname -m
cd ~/Downloads
tar -xzf Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2.tar.gz
cd Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.2
./install.sh
commander-client setup
commander-client status
```

Für die GUI das passende `GUI-...tar.gz` aus der Tabelle verwenden und nach dem Entpacken `./install.sh --background on --tray on` ausführen. Bei ARM64 in den Namen `x86_64` durch `arm64` ersetzen. Nach der Installation ggf. neues Terminal öffnen oder `source ~/.bashrc` ausführen.

**Pairing:** HTTPS-Gateway angeben, angezeigten Gerätecode/Link im Browser freigeben. Headless nutzt eine lokale HTTPS-WebUI; das Startpasswort und ein erforderlicher einmaliger Aktivierungscode werden bei der Installation lokal angezeigt. Zertifikats-Fingerabdruck prüfen und Passwort ändern.

### Upgrade von 2.2.1

```bash
meilleur-client update --check
meilleur-client update
commander-client status
commander-client update --check
```

Bestehendes Pairing und Client-State bleiben erhalten. Verfügbar ist ein Update **nur**, wenn das verbundene Gateway der Architektur/Variante den passenden signierten Kanal zugewiesen hat. `commander-client rollback` kehrt bei vorhandenem lokalen Vorgängerslot zurück.

## Prüfungen und Kompatibilität

- Finaler Quellstand: `75ec797ceaa8a14e6be5710e4c9de73789f87749`.
- ARM64 GUI + Headless und x86_64 GUI + Headless: **vier** nativ gebaute, RSA-signierte Varianten, **acht** Release-Artefakte; unabhängige CI und Review bestanden.
- Signaturautorität: `mc-client-caf94007b07dc90b`; Schlüssel verbleibt ausschließlich auf dem Owner-Signierhost.
- **Echter ARM64-Headless-Abnahmetest:** 2.2.1 → 2.2.2 → Rollback 2.2.1, gleiche Geräteidentität, weiterhin verbunden, `commander-client` nach Update nutzbar.
- Ein breiter realer **x86_64-GUI-/Headless-Endkundentest** steht unabhängig von den nativen Build- und Releaseprüfungen noch aus.
- **Synology DSM/QNAP QTS/QuTS hero sind nicht freigegeben**; kein SPK/QPKG enthalten. ARMv7/32-Bit nicht unterstützt. [NAS-Tracking](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1668).
- Für diese 2.2.2-Version gibt es **keine .deb/.rpm-Dateien** in den Release-Assets; ältere separate QA-Pakete nicht verwechseln.

## Anleitungen / Documentation

- [README & Downloadübersicht](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases#readme)
- [Installation, Gateway-Pairing, x86_64-Abnahme und Rollback](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/blob/main/docs/INSTALLATION.md)
- [Fehlerbehebung: PATH, User-systemd, HTTPS, Updatequelle, WebUI](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/blob/main/docs/FEHLERBEHEBUNG.md)
- [Signatur, SHA256 und Zielsysteme](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/blob/main/docs/SICHERHEIT-UND-KOMPATIBILITAET.md)
- [Fehler melden](https://github.com/Meilleur-Tech/Meilleur-Commander/issues), bitte **ohne** Tokens, Kennwörter oder Enrollment-Codes.

**English:** Download the native GUI or Headless TAR.GZ matching your Linux CPU, extract it, and run `./install.sh` as a non-root user. Pair with your HTTPS Gateway using `commander-client setup`. Use `commander-client update --check` for a readable result or add `--json` for automation. The old `meilleur-client` CLI stays compatible. Signed ZIPs are managed update packages, not first-time installers. NAS distributions are **not certified**.
