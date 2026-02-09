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
<img width="604" height="392" alt="image" src="https://github.com/user-attachments/assets/c360548b-c8de-4a51-9566-02bf2f37e8a7" />
<img width="737" height="627" alt="image" src="https://github.com/user-attachments/assets/cf63bdfd-d76c-4506-9a91-dbbbd9874fd8" />







Anschliessend wurde Vagrant eingesetzt, um die VM automatisiert zu erstellen.
Mit einem Vagrantfile wurde definiert, welche Ubuntu-Box verwendet wird, dass Apache automatisch installiert wird und dass eine Portweiterleitung vom Host auf die VM erfolgt.
Nach dem Start der Vagrant-VM war der Apache-Webserver über http://127.0.0.1:8080 erreichbar.

<img width="839" height="365" alt="image" src="https://github.com/user-attachments/assets/9a07eefe-2503-4528-a18d-518c5d57907b" />

<img width="774" height="805" alt="image" src="https://github.com/user-attachments/assets/4338fdcd-cf51-4a08-b161-c520f5319634" />

Nun könnte man hier mit Befehl "sudo nano /var/www/html/index.html" noch die Seite anpassen und Änderungen vornehmen. Ich lasse das gezielt aus und lösche die VM.

Während der Einrichtung traten kleinere Fehler auf (z. B. falsche Box-Bezeichnung oder Syntaxfehler im Vagrantfile), welche analysiert und behoben wurden.
































