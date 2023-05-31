# Deployment

## Application
## Docker image frontend & backend Staging

### Frontend
- Pertama, ke folder frontend lalu pindah ke branch staging. 

- Kemudian salin ***.gitignore*** ke ***.dockerignore***.

- Kemudian membuat ***.env*** (environment) yaitu untuk menghubungkan frontend dan backend.

```
REACT_APP_BASEURL=http://api.yyg.studentdumbways.my.id/api/v1

```

- Kemudian membuat ***Dockerfile*** untuk membuat docker image.

```
FROM node:16-alpine as staging
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start"]
```

- Kemudian build image dengan perintah dibawah ini.

```
docker build -t myyngstwn/be-dumbmerch-staging:latest .
```

![image](Media/Staging/1.png)

### Backend

- Pertama, ke folder backend lalu pindah ke branch staging.  

- Kemudian membuat ***.env*** (environment) yaitu untuk menghubungkan frontend dan backend.

```
 DB_HOST= (ip appserver)
 DB_USER=yyg
 DB_PASSWORD=Katasand1
 DB_NAME=dumbmerch
 DB_PORT=5432 
 PORT=5000

```

- Kemudian membuat ***Dockerfile*** untuk membuat docker image.

```
FROM golang:1.20-alpine
WORKDIR /app   
COPY . . 
RUN go get ./ && go build && go mod download
EXPOSE 5000
CMD ["go", "run", "main.go"]
```

- Kemudian build image dengan perintah dibawah ini.

```
docker build -t myyngstwn/be-dumbmerch-staging:latest .
```

![image](Media/Staging/2.png)

### Deploy Staging

- Pertama, membuat file ***compose.yml*** untuk docker compose.

```
version: "3.8"
services:
   db:
    image: postgres:latest
    container_name: db-dumbmerch
    ports:
      - 5432:5432
    volumes:
      - ~/postgresql:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=yyg
      - POSTGRES_PASSWORD=Katasand1
      - POSTGRES_DB=dumbmerch
   backend:
    depends_on:
      - db
    image: myyngstwn/be-dumbmerch-staging:latest
    container_name: be-dumbmerch
    stdin_open: true
    restart: unless-stopped
    ports:
      - 5000:5000
   frontend:
    image: myyngstwn/be-dumbmerch-staging:latest
    container_name: fe-dumbmerch
    stdin_open: true
    restart: unless-stopped
    ports:
      - 3000:3000
```

- Kemudian jalankan dengan perintah dibawah ini.

```
docker compose up -d
``` 

![image](Media/Staging/3.png)

![image](Media/Staging/4.png)

![image](Media/Staging/5.png)


## Docker image frontend & backend Production

### Frontend
- Pertama, ke folder frontend lalu pindah ke branch production. 

- Kemudian salin ***.gitignore*** ke ***.dockerignore***.

- Kemudian membuat ***.env*** (environment) yaitu untuk menghubungkan frontend dan backend.

```
REACT_APP_BASEURL=http://api.yyg.studentdumbways.my.id/api/v1
```

- Kemudian membuat ***Dockerfile*** untuk membuat docker image.

```
FROM node:16-alpine as staging
WORKDIR /app
COPY . .
RUN npm install

FROM node:16-alpine as production
WORKDIR /app
COPY --from=staging /app /app
EXPOSE 3000
CMD [ "npm", "start"]
```

- Kemudian build image dengan perintah dibawah ini.

```
docker build -t myyngstwn/be-dumbmerch-production:latest .
```

![image](Media/Production/1.png)

### Backend

- Pertama, ke folder backend lalu pindah ke branch production.  

- Kemudian membuat ***.env*** (environment) yaitu untuk menghubungkan frontend dan backend.

```
 DB_HOST= (ip appserver)
 DB_USER=yyg
 DB_PASSWORD=Katasand1
 DB_NAME=dumbmerch
 DB_PORT=5432 
 PORT=5000

```

- Kemudian membuat ***Dockerfile*** untuk membuat docker image.

```
FROM golang:1.20-alpine as staging
WORKDIR /app   
COPY . . 
RUN go get ./ && go build && go mod download

FROM golang:1.20-alpine as production
WORKDIR /app
COPY --from=staging /app /app
EXPOSE 5000
CMD ["go", "run", "main.go"]
```

- Kemudian build image dengan perintah dibawah ini.

```
docker build -t myyngstwn/be-dumbmerch-production:latest .
```

![image](Media/Production/2.png)

### Deploy Production

- Pertama, membuat file ***compose.yml*** untuk docker compose.

```
version: "3.8"
services:
   db:
    image: postgres:latest
    container_name: db-dumbmerch
    ports:
      - 5432:5432
    volumes:
      - ~/postgresql:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=yyg
      - POSTGRES_PASSWORD=Katasand1
      - POSTGRES_DB=dumbmerch
   backend:
    depends_on:
      - db
    image: myyngstwn/be-dumbmerch-production:latest
    container_name: be-dumbmerch
    stdin_open: true
    restart: unless-stopped
    ports:
      - 5000:5000
   frontend:
    image: myyngstwn/be-dumbmerch-production:latest
    container_name: fe-dumbmerch
    stdin_open: true
    restart: unless-stopped
    ports:
      - 3000:3000
```

- Kemudian jalankan dengan perintah dibawah ini.

```
docker compose up -d
``` 

![image](Media/Production/3.png)

![image](Media/Production/4.png)

![image](Media/Production/5.png)

![image](Media/Production/6.png)

![image](Media/Production/7.png)

- Kemudian docker login untuk mempush/menaruh images ke dalam docker hub.

## CI/CD : Jenkins

- Pertama masukkan password yang digenerate Jenkins secara otomatis untuk login sebagai admin.

- Kemudian **select plugin to install**. Dan menambah plugin, yaitu **ssh agent**.

![image](Media/CICD/1.png)

![image](Media/CICD/2.png)

![image](Media/CICD/3.png)

- Kemudian bisa memasukkan `username` dan `password` baru.

![image](Media/CICD/4.png)

![image](Media/CICD/5.png)

- Kemudian membuat ***credentials*** dan menambahkan SSH Private key ke dalam Jenkins.

![image](Media/CICD/6.png)

![image](Media/CICD/7.png)

![image](Media/CICD/8.png)

![image](Media/CICD/9.png)

- Kemudian tambahkan plugin ***Multibranch Scan Webhook Trigger.*** Untuk mengaktifkan trigger pada saat ada update di repository akun github dan ***Discord Notifier*** untuk notifikasi. 

![image](Media/CICD/10.png)

![image](Media/CICD/11.png)

- Kemudian membuat **job** baru frontend. Pilih multibranch pipeline, dikarenakan kita ingin membuat dengan banyak branch.

![image](Media/CICD/12.png)

![image](Media/CICD/13.png)

- Kemudian pilih git untuk repositorynya dan pilih credentials.

![image](Media/CICD/14.png)

- Kemudian mengaktifkan Multibranch Scan Webhook Trigger.

![image](Media/CICD/15.png)

- Kemudian membuat file Jenkins pada masing-masing branch.

***Jenkinsfile staging***

![image](Media/CICD/16.png)

***Jenkinsfile production***

![image](Media/CICD/17.png)

- Kemudian mengaktifkan trigger pada repository akun github ditambahkan di bagian Webhooks.

![image](Media/CICD/18.png)

- Kemudian jalankan **Scan Multibranch Pipeline**.

![image](Media/CICD/19.png)

![image](Media/CICD/20.png)

- Kemudian pada saat muncul centang dan berwarna hijau, maka trigger sudah berjalan dengan baik.

![image](Media/CICD/21.png)

- Dan notifikasi discord berhasil muncul.

![image](Media/CICD/22.png)

- Kemudian Untuk backend langkah-langkahnya sama seperti frontend.

![image](Media/CICD/23.png)

![image](Media/CICD/24.png)

![image](Media/CICD/25.png)

![image](Media/CICD/26.png)

![image](Media/CICD/27.png)

![image](Media/CICD/28.png)

![image](Media/CICD/29.png)

![image](Media/CICD/30.png)

![image](Media/CICD/31.png)

![image](Media/CICD/32.png)

![image](Media/CICD/33.png)

![image](Media/CICD/34.png)