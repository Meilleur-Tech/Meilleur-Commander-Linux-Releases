# Linux 2.2.7 installieren

Öffne den [öffentlichen Linux-2.2.7-Release](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.2.7).
Prüfe im Terminal `uname -m` und wähle das TAR.GZ-Archiv für deine
CPU (x86_64 oder arm64) sowie GUI oder Headless. Entpacke das Archiv und
starte das enthaltene `./install.sh`; danach zeigt
`fclient --help` alle unterstützten Befehle. Mit `fclient connect`
wählst du Hosted-Kundenkonto oder privaten Gateway. Der Gerätecode
wird anschließend ausdrücklich im passenden Konto oder Gateway bestätigt.
Bestehende Pairings werden beim Zielwechsel nicht automatisch entfernt.
Die 20 öffentlichen Assets haben die dokumentierten
[SHA-256-Prüfsummen](SHA256SUMS-2.2.7.txt).
