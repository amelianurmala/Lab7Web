# Lab7Web

# Praktikum PHP Dasar – Program Data Diri  
**Nama:** Amelia Nurmala Dewi  
**NIM:** 312410199  
**Kelas:** TI.24.A.2 
**Mata Kuliah:** Pemrograman Web 1




### 1. Menampilkan Teks Pertama

<img width="1069" height="677" alt="Screenshot (1114)" src="https://github.com/user-attachments/assets/843a2393-576a-4bdb-ae11-f1b722a02243" />


Latihan awal menggunakan fungsi `echo` untuk menampilkan tulisan di browser.

```php
<?php
echo "Hello World";
?>
```

**Penjelasan:**
Kode ini adalah dasar PHP, digunakan untuk memastikan server XAMPP berjalan dan PHP dapat dieksekusi dengan benar.

---

### 2. Menggunakan Variabel

<img width="1366" height="768" alt="Screenshot (1115)" src="https://github.com/user-attachments/assets/cf605fea-1262-499f-a728-9bcc0bf77dc6" />


Selanjutnya digunakan variabel untuk menyimpan data seperti nama dan NIM.

```php
<?php
$nim = "312410199";
$nama = "Amelia Nurmala Dewi";
echo "NIM: $nim <br>";
echo "Nama: $nama";
?>
```

**Penjelasan:**
Variabel di PHP diawali dengan tanda `$`.
Kita bisa menyimpan teks atau angka di dalamnya, lalu menampilkannya dengan `echo`.



### 3. Form Input & $_POST

<img width="1074" height="673" alt="Screenshot (1121)" src="https://github.com/user-attachments/assets/25b14bfd-d734-4b6a-9243-af7f3919f15c" />


Tahap berikutnya adalah membuat form agar pengguna bisa memasukkan data.

```php
<form method="post">
    Nama: <input type="text" name="nama">
    <input type="submit" value="Kirim">
</form>

<?php
if (isset($_POST['nama'])) {
    echo "Selamat Datang, " . $_POST['nama'];
}
?>
```

**Penjelasan:**
Data yang dimasukkan pengguna dikirim menggunakan metode `POST`, dan bisa diakses di PHP dengan `$_POST['nama']`.

---

## 4. Penggabungan Semua Konsep – *Program Data Diri*

<img width="1366" height="675" alt="Screenshot (1125)" src="https://github.com/user-attachments/assets/1e3adad6-548c-445f-8a26-d381c009759f" />


Dari semua latihan di atas, kemudian dibuat satu program utuh yang menggabungkan:

* **Input data** (form HTML)
* **Pengolahan data** (PHP)
* **Logika kondisi** (`if` dan `switch`)
* **Perhitungan aritmatika** (umur dan gaji)
* **Tampilan menarik (CSS)**

Berikut hasil akhirnya 

```php
<?php
// Program Data Diri - PHP Dasar
// Menampilkan hasil hanya setelah tombol kirim ditekan
?>
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Program Data Diri</title>
<style>
    body {
        font-family: 'Segoe UI', Tahoma, sans-serif;
        background: linear-gradient(to bottom right, #7b2ff7, #f107a3);
        color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    .container {
        background: rgba(255,255,255,0.15);
        backdrop-filter: blur(10px);
        padding: 30px;
        border-radius: 15px;
        width: 420px;
        box-shadow: 0 4px 20px rgba(0,0,0,0.25);
    }
    input, select {
        width: 100%;
        padding: 10px;
        margin: 5px 0 15px 0;
        border-radius: 8px;
        border: none;
        outline: none;
    }
    input[type="submit"] {
        background: #9c27b0;
        color: white;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
    }
    input[type="submit"]:hover {
        background: #e91e63;
        transform: scale(1.03);
    }
    .result {
        margin-top: 20px;
        background: rgba(255,255,255,0.2);
        padding: 15px;
        border-radius: 10px;
        animation: fadeIn 0.6s ease-in-out;
    }
    @keyframes fadeIn {
        from {opacity: 0; transform: translateY(20px);}
        to {opacity: 1; transform: translateY(0);}
    }
</style>
</head>
<body>
<div class="container">
<h1>Program Data Diri</h1>

<form method="post" action="">
    Nama:<br><input type="text" name="nama" required>
    Tanggal Lahir:<br><input type="date" name="tgl_lahir" required>
    Pekerjaan:<br>
    <select name="pekerjaan" required>
        <option value="">-- Pilih Pekerjaan --</option>
        <option value="Guru">Guru</option>
        <option value="Programmer">Programmer</option>
        <option value="Dokter">Dokter</option>
        <option value="Wiraswasta">Wiraswasta</option>
        <option value="Mahasiswa">Mahasiswa</option>
    </select>
    <input type="submit" value="Kirim">
</form>

<?php if ($_SERVER["REQUEST_METHOD"] == "POST"): ?>
    <?php
    $nama = $_POST['nama'];
    $tgl_lahir = $_POST['tgl_lahir'];
    $pekerjaan = $_POST['pekerjaan'];

    // Hitung umur
    $lahir = new DateTime($tgl_lahir);
    $hari_ini = new DateTime();
    $umur = $hari_ini->diff($lahir)->y;

    // Tentukan gaji berdasarkan pekerjaan
    if ($pekerjaan == "Guru") $gaji = 4000000;
    elseif ($pekerjaan == "Programmer") $gaji = 8000000;
    elseif ($pekerjaan == "Dokter") $gaji = 12000000;
    elseif ($pekerjaan == "Wiraswasta") $gaji = 5000000;
    else $gaji = 0;

    // Hitung gaji bersih (10% pajak)
    $pajak = 0.1;
    $gaji_bersih = $gaji - ($gaji * $pajak);
    ?>
    <div class="result">
        <h3>Hasil Data Diri</h3>
        Nama: <?= $nama ?><br>
        Tanggal Lahir: <?= $tgl_lahir ?><br>
        Umur: <?= $umur ?> tahun<br>
        Pekerjaan: <?= $pekerjaan ?><br>
        Gaji Kotor: Rp <?= number_format($gaji, 0, ',', '.') ?><br>
        Gaji Bersih: Rp <?= number_format($gaji_bersih, 0, ',', '.') ?><br>
        <hr>
        <?php
        switch ($pekerjaan) {
            case "Guru": echo "Anda seorang pendidik hebat yang mencerdaskan bangsa."; break;
            case "Programmer": echo "Anda pembuat program yang kreatif dan logis."; break;
            case "Dokter": echo "Anda pahlawan kesehatan yang menolong banyak orang."; break;
            case "Wiraswasta": echo "Anda pengusaha mandiri yang berani ambil risiko."; break;
            case "Mahasiswa": echo "Anda calon penerus masa depan yang sedang menuntut ilmu."; break;
            default: echo "Pekerjaan tidak diketahui.";
        }
        ?>
    </div>
<?php endif; ?>
</div>
</body>
</html>
```

---

## 5. Penjelasan Program Akhir

| Bagian                                      | Fungsi                                                                       |
| ------------------------------------------- | ---------------------------------------------------------------------------- |
| `form method="post"`                        | Menyediakan input untuk nama, tanggal lahir, dan pekerjaan                   |
| `$_POST`                                    | Mengambil data dari form                                                     |
| `DateTime` & `diff()`                       | Menghitung umur dari tanggal lahir                                           |
| `if / elseif`                               | Menentukan besaran gaji berdasarkan pekerjaan                                |
| `switch`                                    | Memberikan keterangan tambahan sesuai pekerjaan                              |
| `CSS`                                       | Membuat tampilan gradasi ungu ke pink, transparan, dengan efek animasi halus |
| `if ($_SERVER["REQUEST_METHOD"] == "POST")` | Supaya hasil hanya muncul setelah tombol **Kirim** ditekan                   |






