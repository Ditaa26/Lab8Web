# PHP dan Database MySQL  
## Dita Tiara Putri (312310131)
## TI 23 A1

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
![Screenshot 2024-11-16 113951](https://github.com/user-attachments/assets/ef33c42b-99ee-4484-aa89-f3456787ed8c)  
![image](https://github.com/user-attachments/assets/d78dd1f7-029b-4737-9a8f-558cffd972c2) 
![image](https://github.com/user-attachments/assets/098742fd-1ca1-4816-80f6-173c5810e5b8)  


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

# 1. Membuat file index untuk menampilkan data (Read) (index.php) 
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

# 2 Tambah Barang
```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tambah Barang</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
        }
        h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 20px;
        }
        form {
            margin-top: 20px;
        }
        .input {
            margin-bottom: 15px;
        }
        .input label {
            display: inline-block;
            width: 120px;
            font-weight: bold;
        }
        .input input[type="text"],
        .input input[type="file"],
        .input select {
            width: 200px;
            padding: 5px;
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .submit input {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 5px 15px;
            font-size: 14px;
            cursor: pointer;
        }
        .submit input:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>Tambah Barang</h1>
    <form method="post" action="tambah.php" enctype="multipart/form-data">
        <div class="input">
            <label>Nama Barang</label>
            <input type="text" name="nama" required />
        </div>
        <div class="input">
            <label>Kategori</label>
            <select name="kategori" required>
                <option value="Komputer">Komputer</option>
                <option value="Elektronik">Elektronik</option>
                <option value="Hand Phone">Hand Phone</option>
            </select>
        </div>
        <div class="input">
            <label>Harga Jual</label>
            <input type="text" name="harga_jual" required />
        </div>
        <div class="input">
            <label>Harga Beli</label>
            <input type="text" name="harga_beli" required />
        </div>
        <div class="input">
            <label>Stok</label>
            <input type="text" name="stok" required />
        </div>
        <div class="input">
            <label>File Gambar</label>
            <input type="file" name="file_gambar" />
        </div>
        <div class="submit">
            <input type="submit" name="submit" value="Simpan" />
        </div>
    </form>
</body>
</html>
```
Form untuk Menambah Barang: Ketika kode ini dijalankan di browser, halaman akan menampilkan form yang memungkinkan pengguna untuk menambahkan barang baru ke sistem. Form ini terdiri dari beberapa input field dan tombol submit. 
Form ini akan mengirimkan data ke server untuk disimpan (termasuk data nama barang, kategori, harga, stok, dan gambar) ketika tombol Simpan ditekan.  
Form ini menggunakan metode POST untuk mengirim data ke server dan akan memproses data yang dimasukkan (termasuk mengunggah gambar) ke dalam database yang akan ditangani oleh file PHP ``tambah.php``.  
![image](https://github.com/user-attachments/assets/3a704755-4a21-464c-b975-cd8a2b923dd7) 

# 3 Ubah Barang 
```sh
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;

        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    
    if (!empty($gambar)) {
        $sql .= ", gambar = '{$gambar}' ";
    }
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
}

$id = $_GET['id'];
$sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
if (!$result) die('Error: Data tidak tersedia');
$data = mysqli_fetch_array($result);
function is_select($var, $val) {
    if ($var == $val) return 'selected="selected"';
    return false;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ubah Barang</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
        }
        h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 20px;
        }
        form {
            margin-top: 20px;
        }
        .input {
            margin-bottom: 15px;
        }
        .input label {
            display: inline-block;
            width: 120px;
            font-weight: bold;
        }
        .input input[type="text"],
        .input input[type="file"],
        .input select {
            width: 200px;
            padding: 5px;
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .submit input {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 5px 15px;
            font-size: 14px;
            cursor: pointer;
        }
        .submit input:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>Ubah Barang</h1>
    <form method="post" action="ubah.php" enctype="multipart/form-data">
        <div class="input">
            <label>Nama Barang</label>
            <input type="text" name="nama" value="<?php echo $data['nama']; ?>" required />
        </div>
        <div class="input">
            <label>Kategori</label>
            <select name="kategori" required>
                <option <?php echo is_select('Komputer', $data['kategori']); ?> value="Komputer">Komputer</option>
                <option <?php echo is_select('Elektronik', $data['kategori']); ?> value="Elektronik">Elektronik</option>
                <option <?php echo is_select('Hand Phone', $data['kategori']); ?> value="Hand Phone">Hand Phone</option>
            </select>
        </div>
        <div class="input">
            <label>Harga Jual</label>
            <input type="text" name="harga_jual" value="<?php echo $data['harga_jual']; ?>" required />
        </div>
        <div class="input">
            <label>Harga Beli</label>
            <input type="text" name="harga_beli" value="<?php echo $data['harga_beli']; ?>" required />
        </div>
        <div class="input">
            <label>Stok</label>
            <input type="text" name="stok" value="<?php echo $data['stok']; ?>" required />
        </div>
        <div class="input">
            <label>File Gambar</label>
            <input type="file" name="file_gambar" />
        </div>
        <div class="submit">
            <input type="hidden" name="id" value="<?php echo $data['id_barang']; ?>" />
            <input type="submit" name="submit" value="Simpan" />
        </div>
    </form>
</body>
</html>
```
Formulir ini digunakan untuk mengubah data barang yang ada di database. Pengguna dapat mengedit nama barang, kategori, harga jual, harga beli, stok, dan gambar barang.  
Ketika halaman dibuka, data barang yang akan diubah diambil dari database berdasarkan parameter id yang dikirimkan melalui URL (ubah.php?id=1).  
Query SQL SELECT * FROM data_barang WHERE id_barang = '{$id}' digunakan untuk mengambil data barang berdasarkan ID.  
Query UPDATE data_barang digunakan untuk memperbarui data barang yang dipilih berdasarkan ID (id_barang).  
![image](https://github.com/user-attachments/assets/a52e1f92-3a54-4503-95f6-bba7367c4c5f) 

# 4 Hapus Data
```sh
<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: index.php');
?>
```
![image](https://github.com/user-attachments/assets/9a241b41-ac56-47a5-a7bf-5556e843820c)




















