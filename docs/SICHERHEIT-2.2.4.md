# Fabric Commander Linux 2.2.4 · Sicherheit und Kompatibilität

[Zurück zur Downloadübersicht](../README.md) · [Installation](INSTALLATION-2.2.4.md) · [SHA-256-Prüfsummen](SHA256-2.2.4.md) · [GitHub Latest](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/latest)

## Wie ein Update geprüft wird

Fabric Commander 2.2.4 verwendet für die eigenständige Linux-Updateprüfung **vier öffentliche, architektur- und variantenabhängige Kanaldeskriptoren**: x86_64 und ARM64, jeweils GUI oder Headless. Der Client wählt den zu seiner installierten Variante passenden Kanal. Der Kanal zeigt auf das zugehörige unveränderliche GitHub-Releasepaket. Es ist **keine Verbindung zu einem Gateway und kein Pairing nötig**, um die öffentliche Updatequelle zu prüfen.

Der GitHub-Hinweis **Latest** ist lediglich ein öffentliches Versions- und Downloadsignal, **kein Vertrauensbeweis**. Der Client prüft vor einer Installation die zum Client gehörende RSA-Vertrauenswurzel, den signierten Kanaldeskriptor, das signierte Release-Manifest, die SHA-256-Prüfsumme des exakten ZIP-Pakets sowie Architektur, GUI/Headless-Variante und zulässige Versionsrichtung. Ein falsches oder manipuliertes Paket wird abgelehnt. Rollback steht nur bereit, wenn ein überprüfter vorheriger Installationsstand vorhanden ist.

Die vier signierten Deskriptoren müssen beim Freigeben eines neuen Latest-Releases **gemeinsam und vollständig** zur Verfügung stehen. Ist ein Kanal nicht verfügbar oder stimmt eine Signatur nicht, darf der Client nicht auf eine beliebige oder unsignierte Quelle wechseln. In diesem Fall die Updatequelle prüfen oder den offiziellen Support kontaktieren, nicht Sicherheitsprüfungen umgehen.

## Gateway und Kundenfreigabe

Ein zugewiesener Owner- oder Kundengateway kann zusätzlich bestimmen, **welche bereits veröffentlichte Version** für verwaltete Geräte angeboten wird. Diese optionale Rollout-Policy ist vom öffentlichen Download und von der kryptografischen Paketprüfung getrennt. Für selbständig verwaltete Linux-Clients bleibt die öffentliche signierte Updateprüfung ohne laufenden Gateway nutzbar. Ein Gateway-Release ist nicht erforderlich, damit signierte Linux-Binaries veröffentlicht werden.

## Installation, ältere Versionen und Dateiprüfung

- Für eine Neuinstallation das passende **TAR.GZ-Archiv** verwenden. Die **ZIP-Dateien** sind signierte Updatepakete, keine zweite Installationsmethode.
- Bestehende 2.2.2-/2.2.3-Clients kennen den unabhängigen Updateweg noch nicht. Der Wechsel auf 2.2.4 erfolgt einmalig über den signierten vollständigen Installer; Kopplung und vorhandene Konfiguration vorher sichern und anschließend prüfen. Ab 2.2.4 kann die neue öffentliche Updatequelle verwendet werden, sobald sie vollständig freigegeben ist.
- Original-Download und erwartete SHA-256-Werte stehen in [SHA256-2.2.4.md](SHA256-2.2.4.md). Die RSA-Signaturprüfung des Clients ist zusätzlich erforderlich; ein Hash allein beweist nicht die Identität des Herausgebers.
- `channels/stable.json` ist ein **historischer Index** für ältere Linux-Versionen. Er ist kein aktueller 2.2.4-Vier-Varianten-Kanal und nicht als Ersatz für eine fehlende Signatur zu verwenden.

## Unterstützung und Einschränkungen

2.2.4 stellt native Linux-Binaries für x86_64 und ARM64 bereit, je als GUI und Headless. Ob eine konkrete Distribution oder ein NAS unterstützt wird, hängt zusätzlich von libc, Kernel, Benutzerrechten und Dienstmanager ab. Synology DSM, QNAP QTS/QuTS, ARMv7 und andere 32-Bit-Systeme werden durch diese Pakete **nicht pauschal unterstützt**.

Private Schlüssel, Pairing-Codes und Zugangsdaten gehören nicht in GitHub-Issues. Öffentlich werden nur die für Kunden benötigten Programme, Prüfdaten, Signaturidentitäten und Gebrauchsanleitungen bereitgestellt.
