# Cara instalasi NVM ubuntu

Persiapan:
- Pastikan sudah memiliki arm64 architecture system
- Memiliki user dengan akses sudo
- Koneksi internet yang aktif
- Ubuntu yang mendukung versi 20.04 (Focal), 22.04 (Jammy), 24.04 (Noble) atau yang lebih terbaru

Langkah-langkah instalasi:
- Update repository terlebih dahulu untuk memastikan selalu up-to-date
```bash
sudo apt update
```

- Install Curl untuk mendownload script instalasi
```bash
sudo apt install curl -y
```

- Install nvm dengan menjalankan script ini
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

- Reload terminal session agar script yang baru ditambahkan terbaca
```bash
source ~/.bashrc
```

- Verifikasi apakah nvm sudah terbaca
```bash
nvm --version
```

- Tambahkan node versi LTS atau 22
```bash
nvm install node 22
```
