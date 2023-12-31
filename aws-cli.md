## Mendapatkan Access Key dan Secret Key pada AWS

1. **Masuk ke AWS Console:**
   Akses [AWS Management Console](https://aws.amazon.com/) dan masuk ke akun AWS kamu.

2. **Buka IAM Console:**
   Pergi ke layanan "IAM (Identity and Access Management)" dengan mengklik "Services" dan mencari "IAM".

3. **Navigasi ke Pengguna (Users):**
   Di panel navigasi kiri, pilih "Users". Jika kamu belum membuat pengguna, buat satu.

4. **Pilih Pengguna:**
   Klik pada nama pengguna yang ingin kamu beri akses kunci (access key).

5. **Tab "Security credentials":**
   Beralih ke tab "Security credentials".

6. **Tambahkan Access Key:**
   Di bagian "Access keys", klik "Create access key". Ini akan membuat pasangan access key dan secret key baru untuk pengguna.

7. **Catat Informasi Kunci:**
   Setelah pasangan kunci dibuat, kamu akan melihat access key ID dan secret access key. Simpan informasi ini dengan aman. **Catatan penting:** Secret key hanya akan ditampilkan sekali, jadi pastikan untuk menyimpannya dengan baik.

8. **Konfigurasi AWS CLI:**
   Dengan kunci yang baru dibuat, kamu dapat menggunak


## Konfigurasi Akun AWS
Pertama-tama, kamu perlu mengonfigurasi akun AWS kamu. Gunakan perintah berikut untuk mengatur informasi kredensial seperti access key dan secret key:

```bash
aws configure
```

## Inisialisasi Konfigurasi
Setelah mengonfigurasi akun, inisialisasikan proyek AWS dengan membuat berkas konfigurasi AWS. kamu bisa menggunakan perintah berikut:

```bash
aws configure set region <region-name>
```

## Contoh Penggunaan Perintah CLI
Sekarang kamu dapat menggunakan AWS CLI untuk berbagai tugas. Contohnya, untuk mendapatkan daftar bucket S3, gunakan perintah berikut:

```bash
aws s3 ls
```

## Dokumentasi dan Bantuan
Jangan ragu untuk merujuk ke dokumentasi resmi AWS dan menggunakan opsi --help untuk memahami cara menggunakan perintah secara lebih mendalam:

```bash
aws <command> --help
```

Dengan langkah-langkah di atas, kamu dapat mulai menggunakan AWS CLI untuk mengelola sumber daya cloud kamu dengan mudah. Pastikan untuk mengganti placeholder seperti <region-name> dengan informasi yang sesuai.




