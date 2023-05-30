# Repository

- Pertama,  copy SSH Key `.ssh/id_rsa.pub` pada server dan masukkan kedalam config github dengan membuka https://github.com/settings/keys. Lalu test SSH  connection untuk memastikan bahwa sudah terhubung.

```
ssh -T git@github.com
```
![image](Media/1.png)

![image](Media/2.png)

- Kemudian clone repositori [fe-dumbmerch](https://github.com/demo-dumbways/fe-dumbmerch) & [be-dumbmerch](https://github.com/demo-dumbways/be-dumbmerch). Lalu mengatur ***username*** dan ***email*** di Git untuk pull dan push.

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

- Kemudian masuk ke direktori `fe-dumbmerch` dan mengganti `remote url` menjadi repositori yang dibuat sebelumnya. Setelah itu buat 3 branch baru yaitu **staging**, **production** dan **cicd**. Dan push ke semua branch.

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

