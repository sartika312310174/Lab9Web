# Lab9Web

```
Nama: Sartika Agustin
NIM: 312310174
Kelas: TI.23.A.2
Universitas: Universitas Pelita Bangsa
```
# PRAKTIKUM 9
# Membuat Folder Lab9_php_modular

# Membuat file dengan nama header.php
![image](https://github.com/user-attachments/assets/5eedd270-fcb7-4851-9c26-200d8cbcf598)
# Membuat file dengan nama footer.php
![image](https://github.com/user-attachments/assets/dc4b44e5-d300-44f1-b657-6da4c7109ad2)
# Membuat file dengan nama home.php
![image](https://github.com/user-attachments/assets/bda7ec0f-73d7-4194-b74f-3aeb03bf98d8)
# Membuat file dengan nama about.php
![image](https://github.com/user-attachments/assets/809f8520-1e4c-4518-b508-fc9d781389e4)
# Tampilan home
![image](https://github.com/user-attachments/assets/60f9bfd4-92e3-468e-833f-c98b429d884d)
# Tampilan about
![image](https://github.com/user-attachments/assets/e4c597af-ab2f-43d8-b433-89a87463cf01)
# Tugas
```
Implementasikan konsep modularisasi
pada kode program praktikum 8 tentang database,
sehingga setiap halamannya memiliki template tampilan yang sama.
```
# TUGAS
# Membuat folder baru bernama lab9_tugas

# Membuat file koneksi.php
![image](https://github.com/user-attachments/assets/967ae13f-5de7-48eb-a1c9-81b0da36002d)
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";
$conn = mysqli_connect($host, $user, $pass, $db, 3306);
if ($conn == false)
{
    echo "Koneksi ke server gagal.";
die();
}
?>
```
# Membuat file header.php
![image](https://github.com/user-attachments/assets/f53a01f2-45fb-43fc-adca-d24089b37483)

```
<?php
include("koneksi.php");

// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contoh Modularisasi</title>
    <link href="style.css" rel="stylesheet" type="text/css" />
    <style>
        table { border-collapse: collapse; width: 60%; }
        th, td { border: 1px solid #ddd; padding: 5px; text-align: left; }
        th { background-color: #f4f4f4; }
    </style>
</head>
<body>
    <div id="container">
        <header>
            <h1>Database</h1>
        </header>
        <nav>
            <a href="home.php">Home</a>
            <a href="tambah.php">Tambah Barang</a>
        </nav>
```


