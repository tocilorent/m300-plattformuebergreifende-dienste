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
## SSH-Debug
SSH ist verbunden, aber das Terminal zeigt keinen Prompt an
→ 100 % ein TTY / Terminal-Problem, kein Server-Problem.

<img width="940" height="805" alt="image" src="https://github.com/user-attachments/assets/3e7b6e80-e557-4798-aad5-0077294abdf2" />




