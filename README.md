# rsyslog
Basic of RSYSLOG Server and Client

# Server
Create a GCP Compute Engine with `Ubuntu 18.04.5 LTS` and Firewall Rule `allow-all`

```
rsyslogd -v
sudo systemctl status rsyslog

sudo vi /etc/rsyslog.conf #enable UDP 

# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")

# at file end add
$template remote-incoming-logs,"/var/log/%HOSTNAME%/%PROGRAMNAME%.log"
*.* ?remote-incoming-logs
& ~

rsyslogd -f /etc/rsyslog.conf -N1

sudo systemctl restart rsyslog

sudo systemctl status rsyslog

netstat -anup
udp        0      0 0.0.0.0:514             0.0.0.0:* 

cd /var/log
```

# Client

```
rsyslogd -v
sudo systemctl status rsyslog

sudo vi /etc/rsyslog.conf 

# at file end add

rsyslogd -f /etc/rsyslog.conf -N1

sudo systemctl restart rsyslog

sudo systemctl status rsyslog

*.* @ip-address-of-rsyslog-server:514   # one @ for UDP
*.* @@ip-address-of-rsyslog-server:514  # two @@ for TCP
```

https://computingforgeeks.com/how-to-configure-rsyslog-centralized-log-server-on-ubuntu-18-04-lts/
