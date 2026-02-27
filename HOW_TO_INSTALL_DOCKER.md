# Cara instalasi docker di ubuntu

Persiapan:
- Pastikan sudah memiliki arm64 architecture system
- Memiliki user dengan akses `sudo`
- Koneksi internet yang aktif
- Ubuntu yang mendukung versi 20.04 (Focal), 22.04 (Jammy), 24.04 (Noble) atau yang lebih terbaru

# Langkah-langkah instalasi
- Siapkan lisensi dan alat yang dibutuhkan
```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

- Tambahkan GPG key dan repository resmi dari docker
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Install docker engine
```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- Verifikasi apakah docker sudah terinstall dan jalankan
```bash
sudo docker run hello-world
```

- Setelah instalasi berhasil berikan akses docker tanpa menggunakan sudo
```bash
sudo usermod -aG docker ${USER}
```

