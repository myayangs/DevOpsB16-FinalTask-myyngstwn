# Web Server

## Create Domain

- Pertama membuat semua domain menggunakan platform Cloudflare, dan semua IP akan diarahkan ke IP publik server Gateway.

![image](Media/1.png)

- Kemudian membuat reverse-proxy pada setiap server.

```
#appserver-frontend
server {
    server_name yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.67:3000;
    } 
}

#appserver-backend
server {
    server_name api.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.67:5000;
    }
}

#node-appserver
server {
    server_name node-app.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.67:9100;
    }
}


#Jenkins-CICD
server {
    server_name cicd.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.196:8080;
    }
}

#node-CICD
server {
    server_name node-cicd.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.196:9100;
    }
}

#node-gateway
server {
    server_name node-gateway.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.224:9100;
    }
}

#node-monitoring
server {
    server_name node-monitoring.yyg.studentdumbways.my.id;

    location / {
            proxy_pass http://10.32.142.73:9100;
    }
}

#prometheus
server {
    server_name prom.yyg.studentdumbways.my.id;
    location / {
            proxy_pass http://10.32.142.73:9090;
    }

}

#grafana
server {
    server_name dashboard.yyg.studentdumbways.my.id;
    location / {
            proxy_set_header Host dashboard.yyg.studentdumbways.my.id;
            proxy_pass http://10.32.142.73:3000;
    }
}
```

## SSL Certbot using wildcard

- Kemudian install Certbot terlebih dahulu. Untuk menginstal Certbot, dapat mengikuti dokumentasi yang disediakan [cerbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal&tab=wildcard).

![image](Media/2.png)

- Kemudian membuat dan menginstal sertifikat dengan perintah dibawah ini.

```
sudo certbot certonly \
--manual \
--preferred-challenges=dns \
--email (your-email).com \
--server https://acme-v02.api.letsencrypt.org/directory \
--agree-tos \
-d *.yyg.studentdumbways.my.id
```

![image](Media/3.png)

![image](Media/4.png)

![image](Media/5.png)

- Semua domain sekarang dilindungi dengan sertifikat SSL.

![image](Media/6.png)

![image](Media/7.png)

![image](Media/8.png)

![image](Media/9.png)

![image](Media/10.png)

![image](Media/11.png)
