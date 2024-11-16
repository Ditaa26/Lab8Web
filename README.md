# PHP dan Database MySQL  
# Dita Tiara Putri (312310131)
# TI 23 A1

# Menjalankan MYSQL
![image](https://github.com/user-attachments/assets/bbdc13bc-e1ef-4c22-bbc0-38559e8eb9af)  

# Membuat Database, Membuat Tabel, Menambahkan Data
```sh
CREATE DATABASE latihan1;
CREATE TABLE data_barang (
id_barang int(10) auto_increment Primary Key,
kategori varchar(30),
nama varchar(30),
gambar varchar(100),
harga_beli decimal(10,0),
harga_jual decimal(10,0),
stok int(4)
);
INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);
```
Membuat database baru bernama latihan1.  
Membuat tabel data_barang untuk menyimpan informasi barang.  
Menambahkan tiga data awal tentang produk elektronik ke dalam tabel.  
![Screenshot 2024-11-16 113928](https://github.com/user-attachments/assets/7da80f80-ad95-4327-91c2-1da7b67fc0ef)  
![image](https://github.com/user-attachments/assets/098742fd-1ca1-4816-80f6-173c5810e5b8)  
![Screenshot 2024-11-16 113951](https://github.com/user-attachments/assets/ef33c42b-99ee-4484-aa89-f3456787ed8c)  

# Membuat Program CRUD
![image](https://github.com/user-attachments/assets/2aec6f65-deed-4391-8f60-d9e9a41f152a)  
Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL: http://localhost/lab8_php_database/  
![image](https://github.com/user-attachments/assets/0d4410f3-df74-4c60-98a5-e5c05f6f5174)  

# 1 Membuat file koneksi database (koneksi.php) 
```sh
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";

$conn = mysqli_connect($host, $user, $pass, $db);

if ($conn == false) {
    echo "Koneksi ke server gagal.";
    die();
} else {
    echo "Koneksi berhasil";
}
?>
```
File koneksi.php memastikan aplikasi dapat berkomunikasi dengan database latihan1.  
Jika koneksi berhasil, program dapat melanjutkan operasi database, seperti membaca, menulis, atau memperbarui data. Jika gagal, sistem akan berhenti dan memberikan notifikasi.  
![image](https://github.com/user-attachments/assets/69c43460-65b3-4f3a-8a61-fc9c2d9aa2b6) 

# Membuat file index untuk menampilkan data (Read) (index.php) 















