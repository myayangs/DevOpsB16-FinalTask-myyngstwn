# Monitoring
## Monitor resources for Appserver, CI/CD & Gateway

- Ini adalah node-expoter dari ketiga server.

![image](Media/1.png)

- Kemudian node-exporter dimonitoring oleh Prometheus.

![image](Media/2.png)

- Kemudian setup ***data sources*** grafana yaitu prometheus yang berfungsi sebagai sumber datanya.

![image](Media/3.png)

![image](Media/4.png)

![image](Media/5.png)

## Full Working dashboard in Grafana
### Template Dashboard

- kemudian membuat dashboard menggunakan template. Disini menggunakan template [Node Exporter Full](https://grafana.com/grafana/dashboards/1860-node-exporter-full/).

![image](Media/6.png)

![image](Media/7.png)

![image](Media/8.png)

![image](Media/9.png)

### Alerting Dashboard

- Pertama, memasukkan ***contact point*** untuk alerting. Disini menggunakan ***contact point*** alerting Discord.

![image](Media/10.png)

- Kemudian membuat ***alert rules*** untuk CPU, RAM dan Disk.

![image](Media/11.png)

![image](Media/12.png)

![image](Media/13.png)

- Discord notifikasi sudah berhasil.

![image](Media/14.png)

