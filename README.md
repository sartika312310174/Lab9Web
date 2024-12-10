# Lab9Web

```
Nama: Sartika Agustin
NIM: 312310174
Kelas: TI.23.A.2
Universitas: Universitas Pelita Bangsa
```
# PRAKTIKUM 9
# Membuat Folder Lab9_php_modular
![image](https://github.com/user-attachments/assets/15d970e0-08fe-4d94-bfb0-42cf35103983)
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
![image](https://github.com/user-attachments/assets/2e421a19-12da-466f-bcab-92d4e38719cf)
# Membuat file koneksi.php
![image](https://github.com/user-attachments/assets/967ae13f-5de7-48eb-a1c9-81b0da36002d)
# Membuat file header.php
![image](https://github.com/user-attachments/assets/f53a01f2-45fb-43fc-adca-d24089b37483)
# Membuat file footer.php
![Screenshot (67)](https://github.com/user-attachments/assets/509122fc-ac60-4d52-b6e9-2ec73116d9cf)
# Membuat file tambah.php
![image](https://github.com/user-attachments/assets/8512cd42-ee0c-4b33-8323-d90a6eb1137a)
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_',$file_gambar['name']);
        $destination = dirname(__FILE__) .'/gambar/' . $filename;
        if(move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }
    
    $sql = 'INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar) ';
    $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}','{$harga_beli}', '{$stok}', '{$gambar}')";
    $result = mysqli_query($conn, $sql);
    header('location: home.php');
}
?>

<?php require('header.php'); ?>

<div class="content">
    <h1>Tambah Barang</h1>
    <div class="main">
        <form method="post" action="tambah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" style="margin-left: 20px;" />
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;" >
                    <option value="Komputer">Komputer</option>
                    <option value="Elektronik">Elektronik</option>
                    <option value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" style="margin-left: 40px;" />
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" style="margin-left: 43px;" />
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" style="margin-left: 85px;" />
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>

<?php require('footer.php'); ?>
```
# Membuat file ubah.php
![image](https://github.com/user-attachments/assets/1af284d1-f992-425d-a6ce-1ca52b50b33c)
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    if (!empty($gambar))
        $sql .= ", gambar = '{$gambar}' ";
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);

    header('location: home.php');
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

<?php require('header.php'); ?>

<div class="content">
    <h1>Ubah Barang</h1>
    <div class="main">
        <form method="post" action="ubah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" value="<?php echo $data['nama'];?>" style="margin-left: 20px;"/>
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;">
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" value="<?php echo $data['harga_jual'];?>" style="margin-left: 40px;"/>
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" value="<?php echo $data['harga_beli'];?>" style="margin-left: 43px;"/>
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" value="<?php echo $data['stok'];?>" style="margin-left: 85px;"/>
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="hidden" name="id" value="<?php echo $data['id_barang'];?>" />
                    <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>

<?php require('footer.php'); ?>
```
# Membuat file hapus.php
![image](https://github.com/user-attachments/assets/003c1156-270c-4b79-87a1-2327dc9322a9)
# TAMPILAN HOME
Cara mengaksesnya dengan masuk ke url http://localhost/lab9_tugas/home.php
![Gambar WhatsApp 2024-12-10 pukul 13 44 20_00da7823](https://github.com/user-attachments/assets/f2e74c6f-8853-4ae9-af6d-2f359f1b9662)
# TAMPILAN TAMBAH BARANG
![image](https://github.com/user-attachments/assets/82716527-6962-437a-bccb-0c80c5cb11d7)
# Membuat file about.php
![image](https://github.com/user-attachments/assets/656e7c79-9e6c-47e1-881e-10545a7405df)
# TAMPILAN about
![Gambar WhatsApp 2024-12-10 pukul 13 44 38_3e09c872](https://github.com/user-attachments/assets/e009f66b-76fc-4a6a-a674-90be5b6dad17)


