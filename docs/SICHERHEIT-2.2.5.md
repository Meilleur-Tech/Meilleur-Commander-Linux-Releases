# Fabric Commander Linux 2.2.5 · Sicherheit und Kompatibilität

[Downloads](../README.md) | [Änderungen](RELEASE-NOTES-2.2.5.md) | [Installation](INSTALLATION.md)

Für x86_64 und ARM64 gibt es jeweils getrennte GUI- und Headless-Ausgaben. TAR.GZ ist die native Installationsform, ZIP dient dem signierten Update. Jedes Kundenpaket und seine Metadaten sind an Architektur, Variante, Clientversion, signierten Quellstand und SHA-256 gebunden. Die zusätzlichen signierten Linux-Kanaldeskriptoren und Manifeste werden mit dem vertrauenswürdigen RSA-SHA256-Schlüssel geprüft (öffentliche Schlüsselidentität mc-client-caf94007b07dc90b). Der private Signierschlüssel gehört nicht in die öffentliche Verteilung und nicht in ein Kundenpaket.

Bei der Hosted-Anmeldung startet der Kunde commander-client account connect und bestätigt einen kurzlebigen Code auf einem anderen Browsergerät. Niemand sollte Codes, Tokens, Passwörter oder Kontodaten öffentlich posten. Die private Gateway-Kopplung bleibt separat. Linux-OTA benötigt keinen Gateway-2.2-Release; es prüft GitHub Latest und signierte Kanal- und Paketdaten. Bereits installierte 2.2.4-Clients verwenden für ihren ersten Übergang weiterhin ihren bisherigen signierten Kanal.

Keine Prüfung per --force umgehen, keine fremde GUI-/Headless- oder CPU-Variante installieren, keine inoffiziellen NAS-Pakete voraussetzen. Ein Rollback ist nur auf einen vorher vorhandenen Installationsslot möglich. Die SHA-256-Werte werden zusammen mit den tatsächlichen signierten 2.2.5-Artefakten veröffentlicht und müssen zum heruntergeladenen Release passen.
