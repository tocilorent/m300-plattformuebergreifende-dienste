# Self-Hosted Cloud mit Nextcloud & Monitoring
## Projektübersicht
In diesem Projekt wird eine containerisierte Self-Hosted-Cloud-Lösung auf Basis von Docker realisiert.
Ziel ist es, einen produktionsnahen Dienst bereitzustellen, der in einer virtualisierten Umgebung betrieben wird und zentrale Aspekte wie Netzwerk, Persistenz, Sicherheit und Monitoring berücksichtigt.

Als Applikation wird Nextcloud eingesetzt. Nextcloud ist eine Open-Source-Plattform zur Dateiablage und Zusammenarbeit und stellt eine selbst gehostete Alternative zu Cloud-Diensten wie Google Drive oder OneDrive dar.

Die Lösung wird innerhalb einer Vagrant-VM unter Ubuntu betrieben und vollständig containerisiert umgesetzt.

## Ziel des Projekts 

Ziel dieses Projektes ist es:

- Einen produktionsnahen Docker-Dienst zu betreiben
- Frontend und Backend logisch zu kombinieren
- Eine saubere Netzwerkstruktur zu konfigurieren
- Persistente Datenspeicherung mittels Volumes zu implementieren
- Eine Monitoring-Lösung zur Überwachung der Container einzusetzen
- Fehler systematisch zu dokumentieren und zu beheben
- Das Projekt soll zeigen, wie moderne Dienste containerisiert bereitgestellt, strukturiert konfiguriert und kontrolliert überwacht werden können.

## Geplante Architektur 

Die Architektur basiert auf einer klaren Trennung der Komponenten:

- Hostsystem: Notebook mit Vagrant & VirtualBox
- Virtuelle Maschine: Ubuntu 16.04
- Containerisierung: Docker Engine
- Frontend: Nextcloud Container
- Backend: MariaDB Container
- Monitoring: cAdvisor Container
- Netzwerk: Docker internes Netzwerk
- Persistenz: Docker Volumes



# Dokumentation

## Docker testen
Ich bin im richtigen Docker drin und er läuft korrekt, jedoch läuft noch mein alter Container. Damit das Projekt reibungslos verlaufen kann, erstelle ich sicherheitshalber eine saubere Umgebung.
<img width="901" height="180" alt="image" src="https://github.com/user-attachments/assets/e52670d9-f01e-4390-967a-1820354cdfe1" />

Das Ganze wurde nun aufgeräumt
<img width="936" height="216" alt="image" src="https://github.com/user-attachments/assets/d946b514-5407-408a-8de6-a15f40e74447" />

## Fehler bei Erstellung von Nextcloud
### MariaDB starten
<img width="939" height="441" alt="image" src="https://github.com/user-attachments/assets/711fcb5e-f6c4-491c-9164-c3cdf95da248" />

Der Container restartet ständig -> also ist wahrscheinlich etwas falsch in der MariaDB Initialisierung. Die Datenbank startet -> crashed -> startet wieder neu
#### Fehler erkannt: 
- In den Logs nachgeschaut (docker logs nc_db)
- Problem war nicht die Konfiguration, sondern dass meine Xenial VM zu alt ist
#### Fehlerbehebung:
- Container komplett löschen und richtiges Image verwenden, statt mariadb:10.6 verwende ich nun mariadb:10.3
Ergebnis -> Kein Restarting mehr, läuft nun sauber und korrekt
<img width="941" height="134" alt="image" src="https://github.com/user-attachments/assets/5e52dcb3-72dc-4cce-8277-9fe5055fc380" />

### Nextcloud Container starten
#### Fehler erkannt:
Beim booten meiner Vagrant Xenial VM kam immer eine SSH-Fehlermeldung. Es gab immer einen Timeout. Ich habe mein PC neugestartet, Netzwerkadaptereigenschaften geändert und die VM mehrfach gelöscht und wieder gebootet. Jedoch nützte das alles nicht.
#### Fehlerbehebung
<img width="746" height="453" alt="image" src="https://github.com/user-attachments/assets/f63ee692-82a8-4f8f-a739-5c65adffdeb2" />


Der Fehler liegt an Xenial. Die Version ist alt. Ich bin daher auf Yammy umgestiegen, in dem ich das im Vagrantfile geändert habe. (config.vm.box = "ubuntu/jammy64") -> Nun funktioniert die VM sowie Docker reibungslos.

<img width="709" height="164" alt="image" src="https://github.com/user-attachments/assets/d2c8e35f-1d0e-4e1b-becb-c14b8b9bb0ac" />

--FEHLER LIEGT HÖCHSTWAHRSCHEINLICH BEI VAGRANT--
In der Vagrant/Xenial VM gab es reproduzierbare Probleme (Logs + Fehlerauszug).
Ich umgehe das in dem ich die Docker-Desktop Version benutze und dort ein Compose erstelle
Ziel ist Containerisierung + Networking + Volumes + Monitoring.

## Neuanfang 
Docker gestartet


<img width="619" height="35" alt="image" src="https://github.com/user-attachments/assets/4b1a9ccc-124f-48fb-b636-df8930de548e" />

![Uploading image.png…]()











