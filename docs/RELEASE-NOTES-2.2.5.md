# Fabric Commander Linux 2.2.5 · Kundenänderungen

[Linux Downloads](../README.md) | [Installation](INSTALLATION-2.2.5.md) | [Sicherheit](SICHERHEIT-2.2.5.md)

## Hosted CTRL: Headless-Gerät ohne lokalen Browser anmelden

Linux 2.2.5 ermöglicht dem Kunden, die Hosted-Kontoanmeldung auf einem Headless-Linuxserver zu beginnen und die erforderliche Browserbestätigung auf einem separaten Laptop, Desktop oder Smartphone durchzuführen. Der Kunde startet im Linux-Terminal den Befehl commander-client account connect. Der Client zeigt den kurzlebigen Gerätecode und die Bestätigungsadresse. Die Freigabe erfolgt erst nach ausdrücklicher Bestätigung beim richtigen Kundenkonto auf dem anderen Gerät. Das Terminal fragt den Bestätigungszustand selbstständig ab.

Die vorhandene Pairingfunktion eines eigenen privaten Gateways bleibt davon unabhängig. Der neue Hosted-Weg ersetzt keine Autorisierung, keinen Kundenvertrag und kein Sicherheits- oder Kontolimit.

## Unabhängiger, signierter Linux-Updatekanal

Die vier nativen Varianten x86_64 GUI, x86_64 Headless, ARM64 GUI und ARM64 Headless beziehen ihre künftigen Updates eigenständig aus GitHub Latest. Die Dateinamen, SHA-256-Prüfsummen und RSA-Signaturen der Update- und Kanalmanifeste werden für die richtige CPU- und UI-Variante geprüft. Der einmalige Wechsel von bereits installierter Linux-Version 2.2.4 erfolgt weiterhin über deren vorhandenen signierten Kanal, den dieselbe Veröffentlichungsaktion aktualisiert. Gateway 2.2 oder eine manuelle Gateway-Client-Aktivierung ist für einen neuen nativen Linux-Release nicht erforderlich.

## Kompatibilität und Sicherheit

Linux 2.2.5 unterstützt x86_64 und ARM64 mit jeweils eigenständiger GUI- und Headless-Variante. Der signierte Release- und Updatepfad lehnt falsche Architektur, falsche Variante und ungültige RSA-Signaturen ab. Private Gateway-Kopplung und Hosted-Kontoanmeldung sind getrennte Funktionen.

## Installation, Rollback und Grenzen

Neuinstallationen verwenden die passende TAR.GZ-Datei mit Installationsskript. ZIP-Dateien gehören zur signierten Updateversorgung. Die bisherige Linux-Kopplung und Benutzeridentität bleiben beim regulären In-Place-Update erhalten. Bei einem Fehler ist ein Rollback nur auf einen wirklich vorhandenen alten Installationsslot möglich. Eine fremde CPU-Architektur oder GUI/Headless-Variante darf nicht erzwungen werden. Zusätzliche fclient-Systemübersichten, ausführliche ASCII-Verbindungslogs und die VM-Klon-Identitätskorrektur gehören nicht zu diesem begrenzten 2.2.5-Release.

## Geprüfter Quellstand

Für den signierten Linux-2.2.5-Release ist der vollständige native Source SHA `5ff4b37285810637365b8039c5552aee987e572c` vorgesehen. Die tatsächliche Releasefreigabe erfordert genau diesen akzeptierten Source-Stand oder eine vor Veröffentlichung entsprechend aktualisierte, erneut geprüfte SHA.
