# Provisioning

## Terraform
### Setup Terraform

- Buat folder baru dan file baru `main.tf` untuk mengatur konfigurasi Terraform IDCH.

- Kemudian isi `main.tf` buat 4 VM dengan spesifikasi sebagai berikut :

|      VM      |  CPU  |  RAM  | Storage |
|    :---:     | :---: | :---: |  :---:  |
|     App      |   2   | 2 GB  |  20 GB  |
|    CI/CD     |   2   | 2 GB  |  20 GB  |
|   Gateway    |   1   | 1 GB  |  20 GB  |
|  Monitoring  |   2   | 2 GB  |  20 GB  |

```
terraform {
  required_providers {
    idcloudhost = {
      source = "bapung/idcloudhost"
      version = "0.1.3"
    }
  }
}

provider "idcloudhost" {
    auth_token = ""
    region = ""
}

resource "idcloudhost_vm" "yyg-appserver" {
    name = "yyg-appserver"
    os_name = "ubuntu"
    os_version= "20.04"
    disks = 20
    vcpu = 2
    memory = 2048
    username = "yyg"
    initial_password = "" 
    billing_account_id = 
    public_key = "" 
    backup = false
}

resource "idcloudhost_floating_ip" "ip-yyg-appserver" {
    name = "yyg-appserver"
    billing_account_id = 
    assigned_to = idcloudhost_vm.yyg-appserver.id
}


resource "idcloudhost_vm" "yyg-cicd" {
    name = "yyg-cicd"
    os_name = "ubuntu"
    os_version= "20.04"
    disks = 20
    vcpu = 2
    memory = 2048
    username = "yyg"
    initial_password = "" 
    billing_account_id =  
    public_key = "" 
    backup = false
}

resource "idcloudhost_floating_ip" "ip-yyg-cicd" {
    name = "yyg-cicd"
    billing_account_id =  
    assigned_to = idcloudhost_vm.yyg-cicd.id
}

resource "idcloudhost_vm" "yyg-gateway" {
    name = "yyg-gateway"
    os_name = "ubuntu"
    os_version= "20.04"
    disks = 20
    vcpu = 1
    memory = 1024
    username = "yyg"
    initial_password = "" 
    billing_account_id =
    public_key = "" 
    backup = false
}

resource "idcloudhost_floating_ip" "ip-yyg-gateway" {
    name = "yyg-gateway"
    billing_account_id =  
    assigned_to = idcloudhost_vm.yyg-gateway.id
}

resource "idcloudhost_vm" "yyg-monitoring" {
    name = "yyg-monitoring"
    os_name = "ubuntu"
    os_version= "20.04"
    disks = 20
    vcpu = 2
    memory = 2048
    username = "yyg"
    initial_password = "" 
    billing_account_id =  
    public_key = "" 
    backup = false
}

resource "idcloudhost_floating_ip" "ip-yyg-monitoring" {
    name = "yyg-monitoring"
    billing_account_id =  
    assigned_to = idcloudhost_vm.yyg-monitoring.id
}

```

- Kemudian lakukan perintah `terraform init` menginisialisasi direktori kerja yang berisi file konfigurasi Terraform.

![image](Media/Terraform/1.png) 

- Kemudian lakukan perintah `terraform plan` membuat rencana eksekusi, yang memungkinkan melihat pratinjau perubahan yang akan dilakukan Terraform pada infrastruktur.

![image](Media/Terraform/2a.png)

![image](Media/Terraform/2b.png)

- Kemudian lakukan perintah `terraform apply` mengeksekusi tindakan yang diusulkan dalam rencana Terraform.

![image](Media/Terraform/3a.png)

![image](Media/Terraform/3b.png)

![image](Media/Terraform/3c.png)

- Dan memeriksa VM telah berhasil dibuat menggunakan Terraform.

![image](Media/Terraform/4.png)

![image](Media/Terraform/5.png)

![image](Media/Terraform/6.png)

![image](Media/Terraform/7.png)

## Ansible
### Setup Ansible

- Pertama untuk menyiapkan **Ansible** adalah membuat `Inventory` (yang berisi dengan IP/Host dari server yang akan di koneksikan dengan Ansible) dan `ansible.cfg` (yang berisi konfigurasi dasar Ansible).

![image](Media/Ansible/1.png)

- Kemudian membuat file `ansible playbook` berdasarkan kebutuhan untuk instalasi di dalam VM.

### Install Docker & Node Exporter

- Untuk menginstall `Docker` dan `Node Exporter` on top docker di semua server. buat file `ansible playbook` terlebih dahulu. Kemudian jalankan menggunakan perintah dibawah ini.

```
ansible-playbook (nama-file).yml
```

![image](Media/Ansible/2.png)

![image](Media/Ansible/3.png)

- `Docker` dan `Node Exporter` sudah terinstall di masing-masing VM.

![image](Media/Ansible/4.png)

![image](Media/Ansible/5.png)

### Install NGINX & Reverse Proxy

- Sebelum menginstall `nginx` buat file konfigurasi `Reverse Proxy`.

![image](Media/Ansible/6.png)

- Kemudian buat file `nginx` untuk server gateway dan jalankan.

![image](Media/Ansible/7.png)

![image](Media/Ansible/8.png)

- `nginx` sudah terinstall di server gateway.

![image](Media/Ansible/9.png)

### Install Jenkins

- Kemudian buat file `jenkins` on top docker untuk server cicd dan jalankan.

![image](Media/Ansible/10.png)

![image](Media/Ansible/11.png)

- `Jenkins` sudah terinstall di server cicd.

![image](Media/Ansible/12.png)

### Install Prometheus & Grafana

- Kemudian buat file `Prometheus & Grafana` on top docker untuk server monitoring dan jalankan.

![image](Media/Ansible/13.png)

![image](Media/Ansible/14.png)

- `Prometheus & Grafana` sudah terinstall di server monitoring.

![image](Media/Ansible/15.png)

![image](Media/Ansible/16.png)