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

## Vagrant-VM automatisch erstellen
Neuen Ordner erstellt 

<img width="861" height="332" alt="image" src="https://github.com/user-attachments/assets/7be19a09-38d8-4a20-ad86-23090916634f" />

Vagrant-File geändert und folgendes hinzugefügt:
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end

  config.vm.provision "shell", inline: <<-SHELL
    set -o xtrace
    sudo apt-get update
    sudo apt-get -y install apache2 webalizer

    # Test-Traffic erzeugen
    curl http://localhost/ >/dev/null 2>&1 || true
    curl http://localhost/ >/dev/null 2>&1 || true
    curl http://localhost/bad >/dev/null 2>&1 || true

    # Output-Pfad fixen
    sudo sed -i -e "s:/var/www/webalizer:/var/www/html/webalizer:" /etc/webalizer/webalizer.conf
    sudo mkdir -p /var/www/html/webalizer

    # Logs rotieren + Webalizer laufen lassen
    sudo logrotate -f /etc/logrotate.d/apache2
    sudo /etc/cron.daily/webalizer
  SHELL
end

# Testen
VM gestartet (vagrant up) und Test im Browser durchgeführt:
- http://127.0.0.1:8080/
 (Apache)
- http://127.0.0.1:8080/webalizer/
 (Webalizer Report) 

<img width="945" height="994" alt="image" src="https://github.com/user-attachments/assets/4f5d9d16-7799-4df6-afa2-93c5fdd96815" />

<img width="941" height="796" alt="image" src="https://github.com/user-attachments/assets/922d9d6e-710c-48a9-9900-953171e37181" />



