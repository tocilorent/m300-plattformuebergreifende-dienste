\# M300 – Infrastruktur-Automatisierung



\## Ziel

Ziel dieses Kapitels ist es, die Grundlagen von Cloud Computing und Infrastructure as Code (IaC) zu verstehen und den Bezug zur praktisch umgesetzten Toolumgebung herzustellen.



\## Cloud Computing

Cloud Computing beschreibt die Bereitstellung von IT-Ressourcen wie Server, Speicher oder Software über ein Netzwerk. Diese Ressourcen werden nicht lokal installiert, sondern flexibel und bedarfsgesteuert genutzt.



Man unterscheidet dabei drei Modelle:

\- \*\*IaaS (Infrastructure as a Service):\*\* Virtuelle Maschinen, Netzwerke und Speicher werden bereitgestellt, die Verwaltung des Systems erfolgt durch den Benutzer.

\- \*\*PaaS (Platform as a Service):\*\* Eine Plattform zur Ausführung von Anwendungen ohne direkte Serververwaltung.

\- \*\*SaaS (Software as a Service):\*\* Fertige Anwendungen, die direkt genutzt werden können (z. B. Webdienste).



\## Infrastructure as Code

Infrastructure as Code bezeichnet den Ansatz, IT-Infrastruktur nicht manuell, sondern über Konfigurationsdateien zu definieren und automatisiert bereitzustellen.  

Dadurch sind Systeme reproduzierbar, konsistent und schnell neu erstellbar.



Änderungen an der Infrastruktur können versioniert, getestet und jederzeit erneut ausgerollt werden.



\## Vagrant als IaC-Werkzeug

Vagrant ist ein Werkzeug zur automatisierten Erstellung und Verwaltung von virtuellen Maschinen.  

Die gesamte Konfiguration erfolgt über ein sogenanntes \*Vagrantfile\*.



Im Rahmen von Kapitel 10 wurde Vagrant verwendet, um eine Ubuntu-VM automatisiert zu erstellen.  

Dabei wurden:

\- eine definierte Ubuntu-Box verwendet

\- Apache automatisch installiert (Provisioning)

\- eine Portweiterleitung vom Host zur VM eingerichtet



Dies ist ein praktisches Beispiel für Infrastructure as Code, da die Infrastruktur vollständig durch Code beschrieben und reproduzierbar erstellt wurde.



\## Fazit

Durch den Einsatz von Infrastructure as Code und Vagrant kann Infrastruktur schneller, zuverlässiger und nachvollziehbarer bereitgestellt werden.  

Manuelle Installationen werden reduziert und Fehlerquellen minimiert.



