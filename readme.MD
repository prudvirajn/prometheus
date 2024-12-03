# Prometheus

Reference: https://prometheus.io/download/

* move to /opt directory
```
wget https://github.com/prometheus/prometheus/releases/download/v3.0.1/prometheus-3.0.1.linux-amd64.tar.gz
```

* Extract tar file
```
tar -xf prometheus-3.0.1.linux-amd64.tar.gz
```

* Rename if required

```
mv prometheus-3.0.1.linux-amd64 prometheus
```

* Create systemctl service
```
vim /etc/systemd/system/prometheus.service
```

* Enter below info
```
[Unit]
Description=Prometheus Server

[Service]
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

```
systemctl start prometheus
```
```
systemctl enable prometheus
```
```
netstat -lntp
```
* to open prometheus use ip with port 9090 

# In the node we have install node_exporter
```
cd /opt/
```
* Download code
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
```
*Extract file
```
tar -xf node_exporter-1.8.2.linux-amd64.tar.gz
```
* rename
```
mv node_exporter-1.8.2.linux-amd64.tar.gz node_exporter
```
* move directory 
```
cd node_exporter
```
* create config file
```
vim /etc/systemd/system/node_exporter.service
```
* Repalce the code
```
 
[Unit]
Description=Node Exporter

[Service]
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target

```
systemctl restart node_exporter
```
```
systemctl enable node_exporter
```
systemctl status node_exporter
```

# GRAFANA
install inside cd opt/prometheus
```
curl -o gpg.key https://rpm.grafana.com/gpg.key
```
```
sudo rpm --import gpg.key
```
* create yum repos
```
vim /etc/yum.repos.d/grafana.repo
```
* replace the code
```
[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
```

* install grafana

```
sudo dnf install grafana -y
```
```
systemctl daemon-reload
```
```
systemctl start grafana-server
```
```
systemctl enable grafana-server
```
```
netstat -lntp
```
* Take ip address with port to open grafana{3000}