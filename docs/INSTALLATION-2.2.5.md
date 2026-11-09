# Fabric Commander Linux 2.2.5 · Installation

[Downloads](../README.md) | [Änderungen](RELEASE-NOTES-2.2.5.md) | [Sicherheit](SICHERHEIT-UND-KOMPATIBILITAET.md)

Mit uname -m die Architektur des Linux-Gerätes prüfen. x86_64 benötigt x86_64, aarch64 benötigt arm64. Für einen Server ohne Desktop die Headless-TAR.GZ-Datei aus dem offiziellen GitHub Release wählen; für einen Desktop die GUI-TAR.GZ-Datei. Den SHA-256-Wert mit der offiziellen zum Release gehörenden Prüfsummenliste vergleichen. Als normaler Linux-Benutzer entpacken und install.sh ausführen, nicht mit root oder sudo.

Danach im Terminal commander-client status prüfen. Für die Hosted-CTRL-Kontoanmeldung auf einem Headless-Gerät commander-client account connect ausführen. Die gezeigte Verifikationsadresse auf einem **anderen Gerät mit Browser** öffnen, den einmaligen Code eingeben und die Kundenfreigabe bestätigen. Ein lokaler Linux-Browser oder eine grafische Oberfläche ist dafür nicht erforderlich. Für ein eigenes privates Gateway bleibt commander-client setup der passende Kopplungsweg.

Für ein bereits installiertes Linux 2.2.4 können commander-client update --check und commander-client update verwendet werden. Es werden die architektur- und variantenrichtigen signierten Updatekanäle geprüft. Bei Bedarf kann commander-client rollback den vorherigen vorhandenen Installationsstand wiederherstellen. Keine Dateien anderer CPU-Architektur, keine private Schlüsseldatei und keine nicht signierten Updatearchive verwenden.
