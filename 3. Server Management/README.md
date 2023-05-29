# Server Management

- Pertama buat SSH Key pada local server. SSH Key yang akan di gunakan untuk mengakses server tanpa password.

![image](Media/1.png)

## Server Login with SSH Key & Password Login Disable

- Pada saat pembuatan VM di Terraform sudah memasukan SSH Public Key. Dengan cara menyalin SSH Public Key local server ke dalam file `main.tf`. Apabila lupa atau belum memasukan SSH Public Key ke dalam server maka bisa menggunakan `ansible-playbook` tanpa harus login ke dalam server tersebut dan kemudian menonaktifkan login kata sandi pada setiap server juga menggunakan `ansible-playbook`. 

![image](Media/2.png)

![image](Media/3.png)

![image](Media/4.png)

![image](Media/5.png)

![image](Media/6.png)

## Create SSH Config & Use 1 SSH Key 

- 

## UFW Enabled with only Port used allowed