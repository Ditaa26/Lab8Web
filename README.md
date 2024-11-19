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
```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Barang</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
        }
        table, th, td {
            border: 1px solid black;
        }
        th, td {
            padding: 10px;
            text-align: left;
        }
        a {
            text-decoration: none;
            color: blue;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h1>Data Barang</h1>
    <a href="tambah_barang.php">Tambah Barang</a>
    <br><br>
    <table>
        <thead>
            <tr>
                <th>Gambar</th>
                <th>Nama Barang</th>
                <th>Kategori</th>
                <th>Harga Jual</th>
                <th>Harga Beli</th>
                <th>Stok</th>
                <th>Aksi</th>
            </tr>
        </thead>
        <tbody>
            <?php
            $data_barang = [
                [
                    "id" => 1,
                    "gambar" => "HP Samsung Android",
                    "nama" => "HP Samsung Android",
                    "kategori" => "Elektronik",
                    "harga_jual" => 2000000,
                    "harga_beli" => 2400000,
                    "stok" => 5
                ],
                [
                    "id" => 2,
                    "gambar" => "HP Xiaomi Android",
                    "nama" => "HP Xiaomi Android",
                    "kategori" => "Elektronik",
                    "harga_jual" => 1000000,
                    "harga_beli" => 1400000,
                    "stok" => 5
                ],
                [
                    "id" => 3,
                    "gambar" => "HP OPPO Android",
                    "nama" => "HP OPPO Android",
                    "kategori" => "Elektronik",
                    "harga_jual" => 1800000,
                    "harga_beli" => 2300000,
                    "stok" => 5
                ]
            ];

            foreach ($data_barang as $barang) {
                echo "<tr>
                        <td>{$barang['gambar']}</td>
                        <td>{$barang['nama']}</td>
                        <td>{$barang['kategori']}</td>
                        <td>{$barang['harga_jual']}</td>
                        <td>{$barang['harga_beli']}</td>
                        <td>{$barang['stok']}</td>
                        <td>
                            <a href='ubah.php?id={$barang['id']}'>Ubah</a> | 
                            <a href='hapus.php?id={$barang['id']}'>Hapus</a>
                        </td>
                    </tr>";
            }
            ?>
        </tbody>
    </table>
</body>
</html>
```

Kode index.php ini menampilkan data barang dalam bentuk tabel dinamis menggunakan PHP, dengan fitur untuk menambah, mengubah, dan menghapus data melalui navigasi tautan, serta menyajikan data langsung dari array.  

![image](https://github.com/user-attachments/assets/20391de8-3c62-4eed-9d72-4225c8a1ce18)
















