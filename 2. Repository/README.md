# Repository

- Pertama, menghubungkan `git` appserver dengan `SSH and GPG Key` github. Dengan cara salin `public key` SSH appserver dan tambahkan ke dalam `SSH Key` github. Setelah itu `Test SSH Connection` dengan perintah dibawah ini.

```
ssh -T git@github.com
```
![image](Media/1.png)

![image](Media/2.png)

- Kemudian clone repository dumbmerch frontend & dumbmerch Backend. Lalu tambahkan Username and Email untuk Pull dan Push.

```
git clone https://github.com/demo-dumbways/fe-dumbmerch
```

```
git clone https://github.com/demo-dumbways/be-dumbmerch
```

![image](Media/3.png)

## Create Private Repository & Branch Repository

### Frontend
- Pertama buat terlebih dahulu private repositori frontend

![image](Media/4.png)

- Kemudian masuk ke direktori `fe-dumbmerch` dan mengganti `remote url` menjadi repositori yang dibuat sebelumnya. Setelah itu buat 3 branch baru yaitu **staging**, **production** dan **cicd***. Dan push ke semua branch.

![image](Media/5.png)

- setelah itu cek pada repositori jika branch sudah di tambahkan.

![image](Media/6.png)

### Backend

- Pertama buat terlebih dahulu private repositori backend

![image](Media/7.png)

- Kemudian masuk ke direktori `be-dumbmerch` dan mengganti `remote url` menjadi repositori yang dibuat sebelumnya. Setelah itu buat 3 branch baru yaitu **staging**, **production** dan **cicd***. Dan push ke semua branch.

![image](Media/8.png)

- setelah itu cek pada repositori jika branch sudah di tambahkan.

![image](Media/9.png)

