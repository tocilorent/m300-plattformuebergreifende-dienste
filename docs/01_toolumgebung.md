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
<img width="1043" height="687" alt="image" src="https://github.com/user-attachments/assets/fadbf146-d411-4d67-a914-041c4d8caea2" />
<img width="976" height="773" alt="image" src="https://github.com/user-attachments/assets/83af43fa-991e-4c07-a9c5-b9af8f68a556" />

VM Ubuntu nun erfolgreich installiert nun das Einrichten:
Im Ubuntu-Terminal folgenden Befehl eingegeben: <img width="615" height="352" alt="image" src="https://github.com/user-attachments/assets/1c99699a-c973-48a6-9d35-cbbc87bec236" />
Anschliessend diesen Befehl eingegeben: <img width="490" height="28" alt="image" src="https://github.com/user-attachments/assets/596422d2-6fe4-4e88-ade8-f37f1f799a54" />
und danach noch diesen Befehl eingegeben: <img width="446" height="26" alt="image" src="https://github.com/user-attachments/assets/cdc582df-2670-42bd-a041-d1e26e55730f" />
Der Apache-Webserver wurde erfolgreich installiert.
Ein grafischer Test über den Browser war aufgrund von Performance-Problemen der VM nur eingeschränkt möglich.
Die erfolgreiche Installation wurde über den Paketmanager (apt) verifiziert.

Vagrant-VM einrichten
<img width="935" height="737" alt="image" src="https://github.com/user-attachments/assets/0bc1fe0d-1231-45c8-8e0f-952b3c8176fb" />
hier musste ich es in der datei von config.vm.box = "ubuntu/xenial164"
 zu config.vm.box = "ubuntu/xenial64" ändern <img width="1353" height="746" alt="image" src="https://github.com/user-attachments/assets/08200e60-b90f-4f94-8d7b-aa4e8f659ace" />
 
vagrant gebootet<img width="732" height="472" alt="image" src="https://github.com/user-attachments/assets/524ce9fa-19c9-4782-9968-495f6ff6add9" />

Einloggen in VM:
<img width="891" height="785" alt="image" src="https://github.com/user-attachments/assets/48f30822-e021-4ff4-b3e5-61d277955215" />
<img width="943" height="599" alt="image" src="https://github.com/user-attachments/assets/a9385fa5-4cac-449a-a4d0-0e675524b1ee" />

Apache automatisch mit Vagrant installieren:
Vagrantfile geändert und folgenden Code eingefügt: <img width="1370" height="565" alt="image" src="https://github.com/user-attachments/assets/d121259b-c84f-4233-b23c-de9cbacd29bf" />

Apache aufgesetzt und ist per Browser erreichbar <img width="927" height="1019" alt="image" src="https://github.com/user-attachments/assets/307e6017-90ab-4862-b1a9-ea69f032ba63" />
Nun könnte man hier mit Befehl "sudo nano /var/www/html/index.html" noch die Seite anpassen und Änderungen vornehmen. Ich lasse das gezielt aus und lösche die VM.







Für die Bearbeitung des Moduls M300 wurde eine lokale Toolumgebung eingerichtet.

Zuerst wurde ein GitHub-Account erstellt und ein öffentliches Repository angelegt.
Zur lokalen Arbeit wurde Git Bash installiert und mit Benutzername sowie E-Mail konfiguriert.
Für die Anmeldung bei GitHub wurde ein SSH-Key erstellt, im GitHub-Account hinterlegt und die Verbindung erfolgreich getestet. Dadurch ist das Arbeiten mit git clone, git commit und git push möglich.

Das Repository wurde lokal geklont und eine Ordnerstruktur für die Dokumentation erstellt.
Änderungen werden regelmässig committet und auf GitHub gespeichert.

<img width="595" height="398" alt="image" src="https://github.com/user-attachments/assets/857315dc-d067-4963-a03a-eb66c4488644" />


Für die Virtualisierung wurde Oracle VirtualBox verwendet.
Eine Ubuntu-VM wurde manuell erstellt, um den klassischen Weg kennenzulernen.
Das System wurde aktualisiert und Apache über den Paketmanager installiert.
Ein grafischer Test über den Browser war aufgrund der Performance der VM nur eingeschränkt möglich, die Installation wurde jedoch erfolgreich durchgeführt.

<img width="810" height="642" alt="image" src="https://github.com/user-attachments/assets/3197ce40-ccc6-4ab1-9a49-ae5915ac6266" />
<img width="508" height="294" alt="image" src="https://github.com/user-attachments/assets/c0d0c90f-329f-4015-8b28-ea3cb265025c" />
<img width="407" height="21" alt="image" src="https://github.com/user-attachments/assets/6c691841-14b1-4585-8939-5b8fee857381" />
<img width="369" height="22" alt="image" src="https://github.com/user-attachments/assets/ec0e5eca-8e6e-410e-8fce-28ee723fb393" />
<img width="775" height="612" alt="image" src="https://github.com/user-attachments/assets/1966f3c6-2ccc-4bd6-bdd3-11cb61b62120" />





Anschliessend wurde Vagrant eingesetzt, um die VM automatisiert zu erstellen.
Mit einem Vagrantfile wurde definiert, welche Ubuntu-Box verwendet wird, dass Apache automatisch installiert wird und dass eine Portweiterleitung vom Host auf die VM erfolgt.
Nach dem Start der Vagrant-VM war der Apache-Webserver über http://127.0.0.1:8080 erreichbar.

Während der Einrichtung traten kleinere Fehler auf (z. B. falsche Box-Bezeichnung oder Syntaxfehler im Vagrantfile), welche analysiert und behoben wurden.


























