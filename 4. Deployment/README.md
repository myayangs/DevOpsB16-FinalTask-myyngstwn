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
      - POSTGRES_PASSWORD=kKatasand1
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


### Docker image frontend & backend Production
## CI/CD

- 