# Fabric Commander Linux 2.2.7 · Änderungen

[Linux-Downloads](../README.md) · [Installation](INSTALLATION-2.2.7.md) · [Sicherheit](SICHERHEIT-2.2.7.md)

## Neu: Hosted oder privater Gateway

Linux 2.2.7 bietet im Terminal mit `fclient connect` und in der
grafischen Oberfläche eine einfache Wahl zwischen Hosted-Kundenkonto und
eigenem privaten Gateway. `fclient connect hosted` benutzt die bestehende
Kundenanmeldung mit Browserfreigabe und Gerätecode. Für den privaten
Gateway bleibt die Kopplung über HTTPS-Adresse und Gerätecode bestehen.
Ein bereits verbundenes Gerät wird bei der Auswahl nicht stillschweigend
getrennt. Es ist ein ausdrückliches Disconnect und anschließendes Pairing
erforderlich. Vorherige Adressen lassen sich wiederverwenden, aber keine
Geräte-Tokens oder Berechtigungen zwischen den Servern übertragen.

## Verbesserte CLI

`fclient --help` zeigt jetzt verständlich die alten Befehle wie
`meilleur-client setup`, `web on/off/status`, `web port set`,
`web password reset`, `status --details`, `status --json`,
`logs` und `uninstall --purge`. Die bisherige Kurzbefehls- und
Headless-Kompatibilität bleibt erhalten. Ungültige Profile erhalten eine
erklärende Fehlermeldung, statt eine bestehende Kopplung zu beschädigen.

## API-freie Updates

Für die öffentliche Update-Suche wird ein statischer HTTPS-Katalog benutzt,
damit mehrere Linux-Clients hinter derselben IP das anonyme GitHub-API-Limit
nicht aufbrauchen. Die Herkunfts-/Signaturprüfung bleibt unabhängig von
diesem Katalog: RSA-signiertes Manifest, SHA-256 und korrekte CPU-Architektur
sowie GUI-/Headless-Variante sind vor jeder Installation erforderlich.
Eine neue signierte Linux-Binary braucht kein Gateway-Release.

## Installation, Kompatibilität, Rollback und Sicherheit

Die vier Varianten sind Linux x86_64 GUI, Linux x86_64 Headless,
Linux ARM64 GUI und Linux ARM64 Headless. Die passende TAR.GZ-Datei ist
für die Neuinstallation bestimmt. ZIP-Dateien sind signierte Updatepakete.
Ein Rollback funktioniert nur zu einem tatsächlich vorhandenen lokalen
Installationsslot. Ein normales Update darf die bestehende Kopplung
nicht absichtlich löschen. Native Build-/Binärtests sind erfolgt,
aber nicht jede Distribution und jede externe Kundeninstallation wurde
damit abgenommen. Es wird weder eine neue Signierinfrastruktur noch
ein extra Gateway-Update verlangt.

## Quellstand

Der genau verwendete native Source SHA lautet
`5a015c01b110353ef40b0e23cf19b74d533ff7de`.
