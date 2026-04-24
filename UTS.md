## Kasus 1 - Audit Direktori dan Backup Aman

**1. Membuat Struktur Direktori**
```bash
mkdir -p ~/uts-os/kasus1/dokumen ~/uts-os/kasus1/log ~/uts-os/kasus1/arsip
```

**2. Membuat dan Mengisi File**
```bash
cat <<EOF > ~/uts-os/kasus1/dokumen/konfigurasi.txt
Setting Server Port: 8080
Database Host: localhost
Max Connection: 100
EOF

cat <<EOF > ~/uts-os/kasus1/dokumen/catatan.txt
Meeting hari ini membahas struktur direktori.
Pastikan semua admin memiliki akses.
Gunakan izin file 640 untuk keamanan.
EOF

cat <<EOF > ~/uts-os/kasus1/log/aplikasi.log
[2026-04-17] INFO: Sistem dimulai.
[2026-04-17] INFO: Mencoba koneksi database.
[2026-04-17] WARN: Penggunaan memori mencapai 70%.
[2026-04-17] ERROR: Gagal memuat file konfigurasi.
[2026-04-17] INFO: Restarting aplikasi.
EOF
```

**3. Mengatur Permission**
```bash
chmod 640 ~/uts-os/kasus1/dokumen/konfigurasi.txt
chmod 750 ~/uts-os/kasus1/dokumen
```

**4. Membuat Symbolic Link**
```bash
ln -s ~/uts-os/kasus1/dokumen/konfigurasi.txt ~/uts-os/kasus1/config-link.txt
```

**5. Membuat dan Verifikasi Arsip**
```bash
cd ~/uts-os
tar -cvzf ~/uts-os/kasus1/arsip/kasus1-backup.tar.gz kasus1/
tar -tvzf ~/uts-os/kasus1/arsip/kasus1-backup.tar.gz
```

---

## Kasus 2 - Shared Folder Tim dan Pengamanan Akses

**1. Membuat Struktur Direktori dan File**
```bash
mkdir -p ~/uts-os/kasus2/kerja/{konfig,log,backup}
touch ~/uts-os/kasus2/kerja/konfig/{app.conf,db.conf}
touch ~/uts-os/kasus2/kerja/log/{server.log,error.log}
```

**2. Mengisi File (Gunakan editor atau echo)**
```bash
echo -e "App_Name=MyApp\nVersion=1.0\nEnv=Production" > ~/uts-os/kasus2/kerja/konfig/app.conf
echo -e "DB_Name=test_db\nUser=admin\nPass=admin123" > ~/uts-os/kasus2/kerja/konfig/db.conf
echo -e "Line 1\nLine 2\nLine 3\nLine 4" > ~/uts-os/kasus2/kerja/log/server.log
echo -e "Log Start\nProcessing data\nERROR: Query failed\nSystem shutdown" > ~/uts-os/kasus2/kerja/log/error.log
```

**3. Atur Permission dan Penjelasan**
```bash
chmod 600 ~/uts-os/kasus2/kerja/konfig/app.conf
chmod 640 ~/uts-os/kasus2/kerja/konfig/db.conf
chmod 700 ~/uts-os/kasus2/kerja/konfig
chmod 750 ~/uts-os/kasus2/kerja/log

cat <<EOF > ~/uts-os/kasus2/penjelasan-permission.txt
Penjelasan Permission:
1. File (600/640): Read/Write menentukan apakah isi file bisa dibaca/diubah.
2. Direktori (700/750): Execute (x) diperlukan untuk masuk ke direktori (cd), 
   sedangkan Read (r) diperlukan untuk melihat daftar file (ls).
EOF

# Bukti tampilan
ls -l ~/uts-os/kasus2/kerja/konfig/app.conf
ls -ld ~/uts-os/kasus2/kerja/konfig
```

**4. Pencarian dan Backup**
```bash
ln -s ~/uts-os/kasus2/kerja/konfig/app.conf ~/uts-os/kasus2/app-link.conf

find ~/uts-os/kasus2 -name "*.conf" > ~/uts-os/kasus2/hasil-pencarian.txt
find ~/uts-os/kasus2 -name "*.log" >> ~/uts-os/kasus2/hasil-pencarian.txt

cp ~/uts-os/kasus2/kerja/konfig/*.conf ~/uts-os/kasus2/kerja/backup/
tar -cvzf ~/uts-os/kasus2/backup-konfig.tar.gz -C ~/uts-os/kasus2/kerja/backup .
tar -tvzf ~/uts-os/kasus2/backup-konfig.tar.gz
```

---

## Kasus 3 - Diagnosis Proses Background

**Bagian A: Job Control**
1. `sleep 400`
2. Tekan `Ctrl + Z` (Hentikan sementara).
3. Ketik `jobs` (Tampilkan daftar job).
4. Ketik `bg %1` (Lanjutkan ke background, sesuaikan angka ID job).
5. Ketik `ps aux | grep sleep` (Tampilkan informasi proses).
6. Ketik `fg %1` (Bawa kembali ke foreground).
7. Tekan `Ctrl + C` (Akhiri proses).

**Bagian B: Prioritas**
1. Terminal 1: `nice -n 0 top` (Default).
2. Terminal 2: `nice -n 15 top` (Prioritas lebih rendah).
3. Lihat kolom `NI` di `top`.
4. Ganti prioritas: `renice -n 5 -p <PID_PROSES>`.
5. Hentikan dengan `kill <PID>` atau tekan `q` lalu `Ctrl+C`.

**Bagian C: Ringkasan**
```bash
cat <<EOF > ~/uts-os/kasus3/ringkasan-proses.txt
Ringkasan Proses:
1. SIGTERM (15): Meminta proses berhenti secara sopan (aman).
2. SIGKILL (9): Menghentikan proses secara paksa (tidak aman, bisa korupsi data).
3. nice: Menentukan prioritas proses saat baru dijalankan (-20 s/d 19).
4. renice: Mengubah prioritas proses yang sudah berjalan.
EOF
```

---

## Kasus 4 - Toolkit Bash dan Arsip Aman

**1. Struktur dan File Contoh**
```bash
mkdir -p ~/uts-os/kasus4/{logs,backup,"ruang nama",sampel}
touch ~/uts-os/kasus4/logs/access-0{1,2,3}.log
touch ~/uts-os/kasus4/sampel/catatan-{a,b}.txt
touch "~/uts-os/kasus4/ruang nama/laporan server april.txt"
touch "~/uts-os/kasus4/ruang nama/backup [mingguan] server.conf"
```

**2. Konfigurasi .bashrc**
```bash
cp ~/.bashrc ~/.bashrc.bak
echo 'export UTS_BASH_DIR=~/uts-os/kasus4' >> ~/.bashrc
echo "alias ll='ls -lah'" >> ~/.bashrc
echo "alias gouts='cd ~/uts-os/kasus4'" >> ~/.bashrc
source ~/.bashrc

# Bukti
echo $UTS_BASH_DIR
type ll
```

**3. Variabel Lokal vs Environment**
```bash
KELAS_UTS="Informatika-A"
echo "Lokal: $KELAS_UTS"
bash -c 'echo "Subshell Lokal: $KELAS_UTS"' # Akan kosong
bash -c 'echo "Subshell Env: $UTS_BASH_DIR"' # Akan muncul
```

**4. Diagnosis dan Wildcard**
```bash
{
  df -h
  free -h
  uptime
  whoami
} > ~/uts-os/kasus4/ringkasan-sesi.txt

# Wildcard aman
ls ~/uts-os/kasus4/logs/*.log
ls ~/uts-os/kasus4/logs/access-0?.log

mkdir ~/uts-os/kasus4/arsip-log
mv ~/uts-os/kasus4/logs/*.log ~/uts-os/kasus4/arsip-log/
tar -cvzf ~/uts-os/kasus4/arsip-log.tar.gz -C ~/uts-os/kasus4 arsip-log
```

**5. File Nama Kompleks dan Refleksi**
```bash
cp "~/uts-os/kasus4/ruang nama/backup [mingguan] server.conf" ~/uts-os/kasus4/backup/backup_mingguan.conf

history | tail -n 15 > ~/uts-os/kasus4/riwayat-bash.txt

cat <<EOF > ~/uts-os/kasus4/refleksi.txt
Refleksi:
Preview wildcard penting untuk memastikan tidak ada file yang salah hapus/pindah.
Quoting (" ") atau escaping (\) wajib digunakan untuk nama file berspasi agar 
bash tidak menganggapnya sebagai dua argumen yang berbeda.
EOF
```
