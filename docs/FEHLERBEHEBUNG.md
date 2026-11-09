# Linux Client 2.2.5 · Fehlerbehebung

[← README](../README.md) · [Installation](INSTALLATION.md) · [Sicherheit & Prüfsummen](SICHERHEIT-UND-KOMPATIBILITAET.md)

## `commander-client: command not found`

Der Installer installiert den Launcher unter `~/.local/bin/commander-client`. Ein bereits geöffnetes Terminal kennt den beim Installieren ergänzten PATH noch nicht.

```bash
source ~/.bashrc
command -v commander-client
~/.local/bin/commander-client status
```

Nach einem **In-Place-Update von 2.2.1 auf 2.2.5** kann der neue Name erst beim regulären Dienststart/Status ergänzt werden. Dann ggf. einmal `meilleur-client status` verwenden und `command -v commander-client` erneut prüfen. Nicht die systemd-Dienste oder State-Verzeichnisse manuell umbenennen.

## `Updatequelle nicht erreichbar`, `manifest_configured=false`, HTTP 404

Ein GitHub-Release allein schaltet ein Update **nicht** frei. Das **gekoppelte Gateway** muss der exakt passenden CPU-Architektur und GUI-/Headless-Variante eine **signierte** Update-URL zuweisen:

```bash
commander-client status --json
commander-client update --check --json
```

Gateway-URL, Geräteidentität, Plattform und Version prüfen. Nicht eigenmächtig den x64-GUI-Kanal in einen ARM64-Headless-Client eintragen, kein `--force`, keine Signaturprüfung umgehen. Bei alten Gateways die Kanalzuweisung vom Betreiber aktualisieren lassen.

## `client is running without a managed lifecycle` / `systemctl --user` fehlgeschlagen

Der Client soll die laufende Bridge bei einem In-Place-Update geordnet über ihren **Benutzer-Dienst** verwalten. Aus einer fremden Root-/VM-Verwaltungssitzung fehlen ggf. `XDG_RUNTIME_DIR` und der D-Bus-User-Bus, obwohl der Dienst korrekt läuft.

**Lösung:** als der normale installierende Linux-Benutzer anmelden, `systemctl --user status meilleur-client.service` und `commander-client status` prüfen. Nicht blind Prozesse beenden, nicht `sudo commander-client update` verwenden und keine Sicherheitsprüfung abschalten.

## Falsche Architektur, `Exec format error` oder fehlende Bibliotheken

```bash
uname -m
```

`x86_64` braucht die x86_64-Datei, `aarch64`/`arm64` die ARM64-Datei. Bei Desktop-Fehlern die normalen Grafik-/Font-/D-Bus-/Qt-Systembibliotheken der Distribution prüfen. Für reine Server **Headless** verwenden, nicht versuchen, eine Desktop-GUI als „Headless“ zu starten. Synology und QNAP werden nicht allein aufgrund des CPU-Typs unterstützt.

## Erstmaliger Headless-WebUI-Zugang / Passwort vergessen

```bash
commander-client web status
commander-client web password reset
```

Die HTTPS-Adresse und den TLS-Zertifikatsfingerabdruck der lokalen Ausgabe entnehmen und vergleichen. Der erstmalige LAN-Zugang erfordert die vom Client angezeigten Zugangsdaten/den einmaligen Aktivierungscode und einen anschließenden Passwortwechsel. Nach erfolgreichem Passwortwechsel bleibt die neue Sitzung angemeldet. Das Webpasswort ist **nicht** für `commander-client update`, `status` oder die CLI-Kopplung erforderlich. Das Gerät niemals allein zur Reparatur des WebUI-Passworts unpairen.

Bei `Forbidden`, `Origin mismatch` oder einem Browser, der keine Aktion zeigt: wirklich die angezeigte HTTPS-Adresse, den konfigurierten Port und Host verwenden. Kein `http://` und keine unkontrollierte Proxy-Host-Weiterleitung. Zertifikat nur nach Fingerabdruckprüfung akzeptieren.

## GUI-Fenster startet, aber kein Tray-Icon

Prüfen, ob die Desktop-Sitzung AppIndicator/KStatusNotifier unterstützt; bei Ubuntu GNOME/Wayland ggf. `ubuntu-appindicators@ubuntu.com` aktivieren und eine neue Sitzung starten. Ohne Host kann die GUI als normales Fenster laufen. Der reine Bridge-Dienst ist unabhängig davon.

## Update erfolgreich, aber Version unverändert / GUI zeigt veraltete Shell

```bash
commander-client status
commander-client status --json
```

Den registrierten Client-Core prüfen, nicht einen noch offenen alten GUI-Prozess. Im Desktop kann ein Fenster-Neustart notwendig sein, damit die Qt-Shell zum neuen Core passt. Ein manuell gestarteter alter Downloadordner ist nicht die installierte Anwendung. Bei Fehlern zuerst den signierten Update-/Rollbackstatus ermitteln.

## Rollback nicht verfügbar

`rollback` setzt einen zuvor installierten, kompatiblen lokalen Slot voraus. Bei frischer Installation oder nach Entfernung des alten Slots ist kein Rollback möglich. Ein Downgrade durch Kopieren eines alten Archivs ersetzt **keinen** signierten Rollback.

## Verbindung oder Pairing fehlgeschlagen

- `commander-client status` zeigt Gateway und Verbindungsstatus. Gateway muss über **HTTPS** erreichbar sein.
- Nur den vom Gateway angezeigten Gerätecode und den zugehörigen Browser-Freigabelink verwenden. Niemals Token oder private Zertifikate in einem Issue posten.
- Bei privater Root-CA muss der Administrator den geprüften Zertifikatsfingerabdruck und CA-Import bereitstellen. Kein `curl -k` als dauerhafter Fix, keine pauschale TLS-Abschaltung.
- `commander-client setup` wiederholen. Nicht zuerst `uninstall --purge` oder `unpair` ausführen: Das würde die Kopplung verändern.

## Diagnose für den Support

Bitte nur **bereinigte** Angaben: Distribution, `uname -m`, GUI/Headless, Clientversion, Gatewayversion soweit öffentlich, exakter reproduzierbarer Fehler und ob es beim Neuinstallieren oder signierten Update auftritt. `commander-client status --json` kann IDs und Umgebungsinformationen enthalten; vor dem Teilen personenbezogene Werte und Gerätemetadaten entfernen. **Nie** Kennwörter, Tokens, Einmalcodes, private CA-Schlüssel oder kompletter State.

[Fehler melden](https://github.com/Meilleur-Tech/Meilleur-Commander/issues).


## Linux 2.2.5: Hosted Headless / account_browser_unavailable

commander-client status muss die Version 2.2.5 anzeigen. commander-client account connect liefert einen Code und eine Bestätigungsadresse, die auf einem anderen Gerät im Browser geöffnet werden. Der Headless-Server benötigt keinen Browser. Die private Gateway-Kopplung über commander-client setup bleibt ein eigener Weg. Für den Übergang von 2.2.4 ist der vorhandene signierte OTA-Kanal vorgesehen, nicht ein unsigniertes Archiv.
