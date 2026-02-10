# M300 – 25 Infrastruktur-Sicherheit

## Ziel
Sicherheit einer virtualisierten Infrastruktur verbessern: Firewall + Reverse Proxy (Apache).

## Setup
Projekt: `vagrant/fwrp`

VMs:
- `proxy` (192.168.56.10): Apache Reverse Proxy + UFW Firewall, Portforwarding Host:8085 → VM:80
- `backend` (192.168.56.11): Apache Webserver (intern)

# Ordnerstruktur im Repo
cd ~/m300-plattformuebergreifende-dienste
mkdir -p vagrant/fwrp

# Vagrant-Projekt für Firewall + Reverse Proxy erstellen
<img width="930" height="303" alt="image" src="https://github.com/user-attachments/assets/0272bea2-946e-4d93-a58c-29d804866bf4" />

Vagrant-File ersetzen mit Folgendem Inhalt:
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  # Proxy VM (Reverse Proxy + Firewall)
  config.vm.define "proxy" do |p|
    p.vm.hostname = "proxy"
    p.vm.network "private_network", ip: "192.168.56.10"
    p.vm.network "forwarded_port", guest: 80, host: 8085, auto_correct: true

    p.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end

    p.vm.provision "shell", inline: <<-SHELL
      set -eux

      apt-get update -y
      apt-get install -y apache2 ufw

      # Apache Reverse Proxy Module aktivieren
      a2enmod proxy proxy_http

      # Reverse Proxy Config
      cat > /etc/apache2/sites-available/001-reverseproxy.conf <<'CONF'
<VirtualHost *:80>
    ServerName localhost

    ProxyRequests Off
    <Proxy *>
        Require all granted
    </Proxy>

    ProxyPass / http://192.168.56.11/
    ProxyPassReverse / http://192.168.56.11/
</VirtualHost>
CONF

      a2dissite 000-default.conf || true
      a2ensite 001-reverseproxy.conf
      service apache2 restart

      # UFW Firewall aktivieren: Default deny incoming
      ufw --force reset
      ufw default deny incoming
      ufw default allow outgoing

      # HTTP erlauben
      ufw allow 80/tcp

      # SSH nur vom Host-only Netz erlauben
      ufw allow from 192.168.56.0/24 to any port 22 proto tcp

      ufw --force enable
      ufw status verbose
    SHELL
  end

  # Backend VM (Webserver intern)
  config.vm.define "backend" do |b|
    b.vm.hostname = "backend"
    b.vm.network "private_network", ip: "192.168.56.11"

    b.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end

    b.vm.provision "shell", inline: <<-SHELL
      set -eux

      apt-get update -y
      apt-get install -y apache2

      echo "<h1>Backend OK</h1><p>Served by backend VM (192.168.56.11)</p>" > /var/www/html/index.html
      service apache2 restart
    SHELL
  end
end

### VM mit "vagrant up" starten
# Funktionstest
## Backend richtig erreichbar? (aus Host)
Per Browser: http://192.168.56.11

<img width="956" height="285" alt="image" src="https://github.com/user-attachments/assets/d46388d4-41f2-4ccb-9317-c6d9538cd2f2" />
## Reverseproxy richtig erreichbar?
<img width="944" height="264" alt="image" src="https://github.com/user-attachments/assets/49c77721-a8c2-4633-83e9-8aa86cc97466" />

# Firewall prüfen
## Fehler im Vagrantfile - Vagrantfile neu aufsetzen
<img width="769" height="94" alt="image" src="https://github.com/user-attachments/assets/cf21206d-5cf2-41f7-906c-d159d498a52a" />

Folgender Inhalt wurde im Vagrantfile eingefügt: 
<img width="769" height="94" alt="image" src="https://github.com/user-attachments/assets/6fb04ee4-7057-4c83-a525-ea0df7e7dc48" />

### Vagrantfile nochmal Testen
<img width="812" height="225" alt="image" src="https://github.com/user-attachments/assets/36deb8b8-c498-4074-ae7b-5cc2e4a1ea60" />
> Nach Fehlerbehebung weitermachen
<img width="778" height="47" alt="image" src="https://github.com/user-attachments/assets/3214a2b1-c2e0-4362-b579-b4cc7603a31f" />

<img width="783" height="310" alt="image" src="https://github.com/user-attachments/assets/8916c277-2b44-4b6f-8c92-16e2677ab4b4" />








