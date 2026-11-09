# Linux 2.2.5 · Sicherheit, Prüfsummen und Kompatibilität

[← README](../README.md) · [Installation](INSTALLATION.md) · [Aktueller Release](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.5)

## Nachprüfbare Release-Daten

| Merkmal | Wert |
|---|---|
| Produkt | Meilleur Commander Client für Linux |
| Version / GitHub-Tag | **2.2.5** / `linux-client-v2.2.5` |
| Native Architekturen | `arm64` (`aarch64`), `x86_64` |
| Separat geprüfte Varianten | GUI und Headless je Architektur |
| Quellcommit für alle vier Varianten | `75ec797ceaa8a14e6be5710e4c9de73789f87749` |
| Signaturalgorithmus | RSA-SHA256, per Release-Manifest |
| Öffentliche Signer-Identität | `mc-client-caf94007b07dc90b` |
| Bridge-Kompatibilität | Protokoll 1; konkrete Gateway-Version wird zusätzlich vom signierten Manifest geprüft |
| Release-Ziel | GitHub Linux **Latest**, kein PROD-Gateway-Deployment |

Der Release wurde nativ auf ARM64 und x86_64 gebaut. Unabhängige CI-/Review-Freigabe für den finalen Quellcommit und offizielle Prüfung der **acht** Artefakte liegen vor. Ein echter ARM64-Headless-In-Place-Test von 2.2.1 nach 2.2.5 und anschließender Rollback auf 2.2.1 wurde mit erhaltener Kopplung erfolgreich durchgeführt. Daraus folgt **nicht**, dass jedes NAS oder jede Linux-Distribution automatisch unterstützt wird.

## SHA-256 aller Assets

Die vollständige maschinenlesbare Liste steht in [SHA256SUMS-2.2.5.txt](SHA256SUMS-2.2.5.txt). Nach dem Download im lokalen Linux-Verzeichnis prüfen:

```bash
sha256sum Meilleur-Commander-Client-Linux-HEADLESS-x86_64-2.2.5.tar.gz
```

Erwartet für dieses Beispiel:

```text
a0fb84952cd12249df1afa278f2c779fe65021ba7d20fb8a4fd37979746c8b43
```

Für eine direkte Listenprüfung die Prüfsummen-Datei und die zu prüfenden Assets in **denselben Ordner** legen und:

```bash
sha256sum -c SHA256SUMS-2.2.5.txt
```

Nicht heruntergeladene Dateien werden von `sha256sum -c` als fehlend gemeldet; bei einem einzelnen heruntergeladenen Archiv am besten dessen einzelnen Hash vergleichen. Bei einer Abweichung **nicht installieren**.

### Aufteilung der acht Dateien

- **4 TAR.GZ-Dateien:** GUI/Headless jeweils ARM64 und x86_64 für eine Neuinstallation mit enthaltenem `install.sh`.
- **4 ZIP-Dateien:** dieselben vier voneinander getrennten **signierten Updatevarianten** für die Gateway-gesteuerte Aktualisierung. Diese ZIP-Dateien nicht als gewöhnliches Desktop-/Headless-Setup verwenden.

Es gibt für 2.2.5 **keine** offiziell freigegebenen `.deb`-/`.rpm`-/`.spk`-/`.qpkg`-Installationsartefakte. Ältere 2.2.0-.deb-Dateien aus einem separaten QA-Preview sind nicht mit diesem 2.2.5-Release gleichzusetzen.

## Vertrauens- und Updatevertrag

1. Der Kunde installiert das zur Architektur passende Originalarchiv über `install.sh` unter **einem normalen Benutzer**; dieses Archiv enthält den nativen Core, die Release-Vertrauensdaten und das lokale Installationsskript.
2. Das Gerät wird durch den vom Gateway ausgegebenen Gerätecode und die Browser-Freigabe gekoppelt. Die Kopplung weist auch die **korrekte Updatevariante** zu.
3. Bei Update, Updateprüfung und Rollback verifiziert der Client signierte Manifestdaten, Paket-Hash, Architektur, GUI-/Headless-Identität, Gateway-/Bridge-Kompatibilität und den gültigen lokalen Updatezustand.
4. Das GitHub-Label **Latest** bietet die Veröffentlichung an, aber der Nutzer kann dadurch **keinen fremden Updatekanal erzwingen**. Fehlende Freigabe im Gateway ist ein konkreter Blocker, kein Anlass zum Ersetzen von URLs oder Abschalten der Prüfung.
5. Der private RSA-Schlüssel liegt auf dem freigabeberechtigten Owner-Signierhost, nicht in diesem öffentlichen Repository, nicht im Linux-Artefakt und nicht auf dem Trusted-Builder.

Der vorherige `meilleur-client`-Befehl, lokale Datenverzeichnisse und die systemd-Dienstnamen bleiben trotz des neuen sichtbaren Namens `commander-client` erhalten; dadurch werden bestehende Kopplungen und Rollbacks nicht durch einen CLI-Rename beschädigt.

## Unterstützte Systeme und Einschränkungen

**Verfügbare native Builds** bedeuten noch keine pauschale Freigabe aller Distributionen. Die Projekt-Tests decken unter anderem Ubuntu-ARM64-Headless und native x86_64-Builds ab. Konkrete Kernel-/glibc-/Display-/User-systemd-Voraussetzungen müssen auf dem Zielsystem vorliegen.

| Umgebung | Status |
|---|---|
| Ubuntu/Debian-artiger Desktop x86_64/ARM64 mit GUI-Abhängigkeiten | Native GUI-Assets verfügbar; Feldtest empfohlen |
| Ubuntu/Debian-artiger Server/VM x86_64/ARM64 mit User-systemd | Native Headless-Assets verfügbar; ARM64-Update/Rollback erfolgreich getestet |
| Synology DSM / QNAP QTS oder QuTS hero | **Nicht freigegeben**. Separates SPK/QPKG-, ABI- und Service-Testing erforderlich |
| ARMv7/ARMhf, 32-bit x86 | **Nicht unterstützt** durch diese 64-Bit-Artefakte |
| Router, Alpine/musl, Minimal-Container oder andere proprietäre Systeme | **Keine Kompatibilitätszusage** ohne konkrete ELF-/Laufzeitprüfung |

Für Synology/QNAP läuft [#1668](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1668). Besonders wichtig: CPU-Instruktionssatz, ELF-Lader/glibc, Kernel-Features, Systemzertifikate, Benutzerrechte und Dienstmanager unterscheiden sich trotz gleicher CPU-Architektur.

## Öffentliches Release-Repository und alte Kanaldatei

Dieses Repository ist **binary-only**. Dokumentation, öffentliche Signaturidentität und Prüfsummen dürfen hier liegen; **keine** privaten Schlüssel, Pairing-Tokens, Geräte-/Accountdaten oder internen Gateway-Secrets.

`channels/stable.json` ist ein **historischer, nicht vertrauenswürdiger Ein-Architektur-Discovery-Index** aus Linux 2.1.0. Er wurde **nicht** heimlich auf 2.2.5 umgeschrieben, weil das vorhandene Schema keine geprüfte Vier-Varianten-Matrix abbildet. Die reale neueste Veröffentlichung findet man über [GitHub Releases / Latest](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/latest); Aktualisierungen werden vom Gateway nach **separater RSA-Prüfung** autorisiert.

## Hinweise zu Versionshistorie und Archiv-README

Frühere Linux-Preview-Dokumente und die `README.txt` **innerhalb älterer oder bereits signierter Bundle-TARs** können veraltete Entwicklungsstände enthalten (etwa „Headless nur Loopback“). Diese bereits signierten Artefakte dürfen nachträglich **nicht** verändert werden, ohne eine neue geprüfte Releaseversion zu erzeugen. Maßgeblich für **2.2.5** sind die hier veröffentlichten Releasehinweise und die aktuelle Kundenanleitung. Bekannte veraltete Bundle-Texte sollten für den **nächsten** signierten Release in der Buildquelle korrigiert werden.


## Linux 2.2.5: unabhängiger, signierter OTA-Kanal

Die vier Varianten x86_64/ARM64 GUI/Headless prüfen signierte Kanaldeskriptoren, Release-Manifeste und SHA-256 des richtigen Pakets. GitHub Latest ist die Updatequelle; Gateway 2.2 ist keine Veröffentlichungsvoraussetzung. Die Bestätigung eines Hosted-CTRL-Gerätecodes erfolgt auf einem anderen Browsergerät. Keine Signatur- oder Architekturprüfung umgehen. Der einmalige signierte 2.2.4-OTA-Übergang wird mit dem Release mitgeführt.
