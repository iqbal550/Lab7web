
# Lab7Web - Praktikum Pemrograman Web PHP Dasar

## Identitas
- Nama: [M. iqbal]
- NIM: [312410212]
- Kelas: [TI.24.A2]

## Tujuan Praktikum
1. Memahami konsep dasar Server Side Scripting
2. Memahami dasar Pemrograman PHP
3. Memahami Variable dan Tipe Data pada PHP
4. Memahami konsep Struktur Kondisi dan Perulangan
5. Mampu membuat program PHP sederhana

## Langkah-Langkah Praktikum

### 1. Persiapan Environment
- Menginstall XAMPP sebagai web server
- Membuat folder `lab7_php_dasar` di `htdocs`
- Menyiapkan text editor (VSCode)

### 2. PHP Dasar
Membuat file `php_dasar.php` untuk belajar sintaks dasar PHP.

**Kode:**
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>PHP Dasar</title>
</head>
<body>
    <h1>Belajar PHP Dasar</h1>
    <?php
    echo "Hello World";
    ?>
</body>
</html>

```

<img width="1918" height="545" alt="Screenshot 2025-11-10 152759" src="https://github.com/user-attachments/assets/9fd3b9e0-342f-4aca-a55b-4522d26d8b61" />

```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Data Diri - Tugas Praktikum 7</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h2 {
            color: #333;
            text-align: center;
            border-bottom: 2px solid #007bff;
            padding-bottom: 10px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background-color: #e7f3ff;
            border-radius: 5px;
            border-left: 4px solid #007bff;
        }
        .result h3 {
            color: #007bff;
            margin-top: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Form Data Diri</h2>
        
        <form method="post">
            <div class="form-group">
                <label for="nama">Nama:</label>
                <input type="text" id="nama" name="nama" required 
                       value="<?php echo isset($_POST['nama']) ? htmlspecialchars($_POST['nama']) : ''; ?>">
            </div>
            
            <div class="form-group">
                <label for="tanggal_lahir">Tanggal Lahir:</label>
                <input type="date" id="tanggal_lahir" name="tanggal_lahir" required 
                       value="<?php echo isset($_POST['tanggal_lahir']) ? $_POST['tanggal_lahir'] : ''; ?>">
            </div>
            
            <div class="form-group">
                <label for="pekerjaan">Pekerjaan:</label>
                <select id="pekerjaan" name="pekerjaan" required>
                    <option value="">-- Pilih Pekerjaan --</option>
                    <option value="Software Engineer" <?php echo (isset($_POST['pekerjaan']) && $_POST['pekerjaan'] == 'Software Engineer') ? 'selected' : ''; ?>>Software Engineer</option>
                    <option value="Data Analyst" <?php echo (isset($_POST['pekerjaan']) && $_POST['pekerjaan'] == 'Data Analyst') ? 'selected' : ''; ?>>Data Analyst</option>
                    <option value="Web Developer" <?php echo (isset($_POST['pekerjaan']) && $_POST['pekerjaan'] == 'Web Developer') ? 'selected' : ''; ?>>Web Developer</option>
                    <option value="System Administrator" <?php echo (isset($_POST['pekerjaan']) && $_POST['pekerjaan'] == 'System Administrator') ? 'selected' : ''; ?>>System Administrator</option>
                    <option value="UI/UX Designer" <?php echo (isset($_POST['pekerjaan']) && $_POST['pekerjaan'] == 'UI/UX Designer') ? 'selected' : ''; ?>>UI/UX Designer</option>
                </select>
            </div>
            
            <button type="submit" name="submit">Proses Data</button>
        </form>

        <?php
        if (isset($_POST['submit'])) {
            // Mengambil data dari form
            $nama = $_POST['nama'];
            $tanggal_lahir = $_POST['tanggal_lahir'];
            $pekerjaan = $_POST['pekerjaan'];
            
            // Menghitung umur
            $tgl_lahir = new DateTime($tanggal_lahir);
            $today = new DateTime();
            $umur = $today->diff($tgl_lahir)->y;
            
            // Menentukan gaji berdasarkan pekerjaan
            $gaji = 0;
            switch ($pekerjaan) {
                case 'Software Engineer':
                    $gaji = 15000000;
                    break;
                case 'Data Analyst':
                    $gaji = 12000000;
                    break;
                case 'Web Developer':
                    $gaji = 10000000;
                    break;
                case 'System Administrator':
                    $gaji = 11000000;
                    break;
                case 'UI/UX Designer':
                    $gaji = 9000000;
                    break;
                default:
                    $gaji = 0;
            }
            
            // Format gaji ke Rupiah
            $gaji_format = "Rp " . number_format($gaji, 0, ',', '.');
            
            // Menampilkan hasil
            echo "<div class='result'>";
            echo "<h3>Hasil Data Diri:</h3>";
            echo "<p><strong>Nama:</strong> " . htmlspecialchars($nama) . "</p>";
            echo "<p><strong>Tanggal Lahir:</strong> " . date('d F Y', strtotime($tanggal_lahir)) . "</p>";
            echo "<p><strong>Umur:</strong> $umur tahun</p>";
            echo "<p><strong>Pekerjaan:</strong> $pekerjaan</p>";
            echo "<p><strong>Gaji:</strong> $gaji_format</p>";
            echo "</div>";
        }
        ?>
    </div>
</body>
</html>
```
<img width="972" height="291" alt="image" src="https://github.com/user-attachments/assets/1f49bb88-271d-4ea9-9853-853a280b5a08" />
<img width="1319" height="840" alt="Screenshot 2025-11-10 154604" src="https://github.com/user-attachments/assets/578f24f3-0efe-4e63-93ca-21780eff367e" />
<img width="1912" height="757" alt="Screenshot 2025-11-10 135607" src="https://github.com/user-attachments/assets/bfd639b8-c8af-4c3f-b331-fe989afc8c92" />


