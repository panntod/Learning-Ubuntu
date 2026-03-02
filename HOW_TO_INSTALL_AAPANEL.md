# Cara instalasi docker di ubuntu

Persiapan:
- Pastikan sudah memiliki arm64 architecture system
- Memiliki user dengan akses sudo
- Koneksi internet yang aktif
- Ubuntu yang mendukung versi 20.04 (Focal), 22.04 (Jammy), 24.04 (Noble) atau yang lebih terbaru

# Langkah-langkah instalasi
- Perbarui repository yang
```bash
sudo apt update && sudo apt upgrade -y
```

- Jalankan script installasi AaPanel
```bash
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh
```

*Catatan: AAPANEL HANYA MENDUKUNG VERSI LTS (22/24), namun kita bisa melakukan bypasss dengan menjalankan:

```bash
nano install.sh
```

dan hapus bagian pengecekan versi ubuntu, CTRL+X > Enter > CTRL+O

- Jalankan `install.sh`
```bash
sudo bash install.sh
```

- Setelah itu simpan dan ingat ingat bagian kredensial ini
```txt
==================================================================
Congratulations! Installed successfully!
==================================================================
aaPanel Internet Address: https://103.113.118.162:27441/bc7ff1e2
aaPanel Internal Address: https://192.168.64.3:27441/bc7ff1e2
username: svs7rezr
password: 34927756
Warning:
If you cannot access the panel, 
release the following port (27441|888|80|443|20|21) in the security group
==================================================================
```

- Lalu release port agar bisa diakses di internet 
```bash
sudo ufw allow 27441
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 21
sudo ufw allow 20
sudo ufw allow 888
sudo ufw reload
```

- Cek apakah port sudah dapat diakses
```bash
sudo ufw status
ss -tulnp | grep 27441
```

- Setelah itu restart
```bash
bt stop
bt start
```

- Masuk ke dalam website https://192.168.64.3:27441/bc7ff1e2 dengan kredensial yang ada dan lakukanlah setup
