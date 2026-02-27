# Cara Menjalankan Containerd.io
Menjalankan containerd.io di Ubuntu dilakukan dengan menginstal paket melalui repositori Docker, mengonfigurasi containerd, dan mengaktifkan layanannya. Langkah utamanya meliputi update sistem, instalasi, pembuatan konfigurasi default, dan memulai layanan (systemctl start containerd). Containerd akan berjalan otomatis saat boot setelah diaktifkan. 

# Instalasi containerd.io
- Perbarui repository dan install containerd.io
```bash
sudo apt-get update
sudo apt-get install -y containerd.io
```

- Konfigurasi containerd
```bash
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
```
Catatan: Modifikasi /etc/containerd/config.toml mungkin diperlukan jika Anda menggunakan Kubernetes (misalnya, mengatur SystemdCgroup ke true).

- Menjalankan dan mengaktifkan layanan
```bash
sudo systemctl enable --now containerd
```

- Verifikasi status
```bash
sudo systemctl status containerd
```

- Mengelola kontainer
  - Menarik Image
  ```bash
  sudo ctr images docker.io/library/nginx:latest
  ```
  
  - Menjalankan kontainer
  ```bash
  sudo ctr run -d docker.io/library/nginx:latest nginx_container
  ```
  
  - Melihat kontainer berjalan
  ```bash
  sudo ctr containers list
  ```
