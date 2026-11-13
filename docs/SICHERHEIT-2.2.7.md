# Linux 2.2.7 · Sicherheit

Vier native GUI-/Headless-Pakete für x86_64/ARM64 sind mit dem bereits
verwendeten RSA-Release-Schlüssel signiert. Der installierte Client
verifiziert beim Update sein signiertes Manifest, SHA-256, Architektur
und die korrekte Variante. Alle 20 öffentlichen Release-Dateien sind
unter [SHA256SUMS-2.2.7.txt](SHA256SUMS-2.2.7.txt) erfasst.
Die öffentlichen Updatekataloge sind Discovery, keine eigenständige
Trust-Autorität. Ein Gateway-Release ist für ein signiertes
Client-Binary nicht erforderlich. Der Wechsel zwischen Hosted und
privatem Gateway verlangt bewusste Trennung und erneute Gerätefreigabe.
Nativer x64-CI-Build und ARM64-Binärtests sind nachgewiesen.
Es wird keine automatische Feldabnahme aller Distributionen behauptet.
