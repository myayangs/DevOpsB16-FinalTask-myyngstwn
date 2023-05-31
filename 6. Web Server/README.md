# Web Server

## Create Domain

- Pertama membuat semua domain menggunakan platform Cloudflare, dan semua IP akan diarahkan ke IP publik server Gateway.

![image](Media/1.png)

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
