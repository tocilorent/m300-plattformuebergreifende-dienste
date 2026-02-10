# M300 – 20 Infrastruktur-Automatisierung

## Ziel
Grundlagen von Cloud Computing, Infrastructure as Code (IaC) und Automatisierung von Infrastruktur verstehen.

---

## 1) Cloud Computing
Cloud Computing bedeutet, dass Rechenleistung, Speicher und Software über ein Netzwerk bereitgestellt und genutzt werden.

### Service-Modelle
- **IaaS (Infrastructure as a Service):** Virtuelle Maschinen, Netzwerke, Storage – Verwaltung liegt beim Nutzer.
- **PaaS (Platform as a Service):** Plattform für Deployments – keine Serververwaltung durch Nutzer.
- **SaaS (Software as a Service):** Fertige Anwendungen, die direkt genutzt werden (z.B. Webmail).

### CaaS (Container as a Service)
Zwischen IaaS und PaaS: Container-Workloads (Docker/Kubernetes) laufen auf bereitgestellter Infrastruktur.

---

## 2) Infrastructure as Code (IaC)
IaC beschreibt Infrastruktur als Code/Definitionen, die versioniert und wiederholbar ausgerollt werden.

**Vorteile:**
- Reproduzierbar und konsistent
- Schnell wiederherstellbar
- Änderungen sind standardisiert und nachvollziehbar (Versionierung)

---

## 3) Vagrant
Vagrant automatisiert die Erstellung von virtuellen Maschinen über ein **Vagrantfile**.

**Wichtige Befehle:**
- `vagrant init` (Vagrantfile erstellen)
- `vagrant up` (VM erstellen/starten)
- `vagrant ssh` (in VM verbinden)
- `vagrant halt` (stoppen)
- `vagrant destroy -f` (löschen)

---

## 4) Packer (optional)
Packer erstellt automatisiert VM-Images (z.B. für VirtualBox, AWS).
- Konfiguration meist als JSON
- kann am Ende z.B. eine Vagrant-Box ausgeben

---

## 5) AWS Cloud (optional)
AWS ist eine Public Cloud (IaaS). Per IAM User + Keys kann man z.B. EC2 Instanzen starten.
Vagrant kann über Plugins auch Instanzen in AWS automatisiert erzeugen.

---

## Reflexion (kurz)
IaC macht Infrastruktur wiederholbar und spart Zeit. Vagrant eignet sich gut für lokale Automatisierung, Packer für eigene Images, AWS für skalierbare Public-Cloud-Umgebungen.
