Toolumgebung – Einrichtung
Ziel

Einrichtung einer funktionsfähigen Toolumgebung zur Bearbeitung des Moduls M300 – Plattformübergreifende Dienste in ein Netzwerk integrieren.

01 - 02 GitHub-Account & Git Client

GitHub-Account erstellt und E-Mail verifiziert

Öffentliches Repository erstellt und initialisiert (README.md)

Git (Git Bash) installiert

Git global konfiguriert mit Benutzername und E-Mail

git config --global user.name "<GitHub-Username>"
git config --global user.email "<GitHub-E-Mail>"

SSH-Key für GitHub

Zur sicheren, passwortlosen Authentifizierung wurde ein SSH-Key verwendet.

Vorgehen:

SSH-Key erstellt:

ssh-keygen -t rsa -b 4096 -C "<GitHub-E-Mail>"


SSH-Agent gestartet und Key hinzugefügt:

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa


Public Key (id_rsa.pub) im GitHub-Account unter SSH and GPG keys hinterlegt

Verbindung erfolgreich getestet:

ssh -T git@github.com

Repository lokal einrichten

Repository per SSH geklont

Arbeiten erfolgen im lokalen Repository-Verzeichnis

git clone git@github.com:<USERNAME>/m300-plattformuebergreifende-dienste.git

Repository-Struktur

Die Grundstruktur des Repositories wurde manuell per Kommandozeile erstellt:

<img width="719" height="479" alt="image" src="https://github.com/user-attachments/assets/3add3d3c-aefd-4e92-988a-5e34010576dc" />

## Git Client (Git Bash)

Für die lokale Arbeit wurde Git for Windows (Git Bash) installiert.

Der Git Client ermöglicht:
- Klonen von Repositories
- Aktualisieren (pull)
- Hochladen von Änderungen (push)

Nach der Installation wurde Git mit dem GitHub-Account konfiguriert:

git config --global user.name "<GitHub-Username>"
git config --global user.email "<GitHub-E-Mail>"

Das Repository wurde erfolgreich per SSH geklont und Änderungen
werden regelmässig mit git add, git commit und git push versioniert.


Diese Struktur ermöglicht eine klare und nachvollziehbare Dokumentation gemäss den Handlungszielen des Moduls.

Versionsverwaltung

Änderungen werden regelmässig versioniert und auf GitHub gespeichert:

git add -A
git commit -m "Toolumgebung und Repository-Struktur erstellt"
git push

03 - Virtualbox 
Virtualbox war bereits installiert 
Schritt 1: Ubuntu Desktop ISO herunterladen

Vagrant installieren und konfigurieren
<img width="280" height="146" alt="image" src="https://github.com/user-attachments/assets/0deb2a78-4c56-47f8-b66e-87dd841a89f4" />

Ubuntu VM erstellen in Virtualbox
<img width="1055" height="542" alt="image" src="https://github.com/user-attachments/assets/c1fa7ac9-2723-4a90-8e66-03d7d80be9f8" />





