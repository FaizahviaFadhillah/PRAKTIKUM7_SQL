#PRAKTIKUM7_SQL

`Nama  : Faizah Via Fadhillah`

`Nim   : 312210460`

`Kelas : TI22.A4`

# ER-D PRAKTIKUM 7

![img.1](gambar/ER-D.png)

# INPUT DATA STUDI KASUS KARYAWAN

![img.2](gambar/Input%20Data.png)

* Script SQL berdasarkan Tabel Perusahaan

    ```sql
    CREATE TABLE Perusahaan(
    id_p VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(45) NOT NULL,
    alamat VARCHAR(45) DEFAULT NULL
    );

    INSERT INTO Perusahaan (id_p, nama, alamat) VALUES
    ('P01', 'Kantor Pusat', NULL),
    ('P02', 'Cabang Bekasi', NULL);
    SELECT * FROM Perusahaan;
    ```

    Output Tabel Perusahaan:

    ![img.3](gambar/1.png)


* Script SQL berdasarkan Tabel Departemen

    ```sql
    CREATE TABLE Departemen(
    id_dept VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(45) NOT NULL,
    id_p VARCHAR(10) NOT NULL,
    manajer_nik VARCHAR(10) DEFAULT NULL
    );

    INSERT INTO Departemen (id_dept, nama, id_p, manajer_nik) VALUES
    ('D01', 'Produksi', 'P02', 'N01'),
    ('D02', 'Marketing', 'P01', 'N03'),
    ('D03', 'RnD', 'P02', NULL),
    ('D04', 'Logistik', 'P02', NULL);
    SELECT * FROM Departemen;
    ```

    Output Tabel Departemen :

    ![img.4](gambar/2.png)


* Script SQL berdasarkan Tabel Karyawan

    ```sql
     CREATE TABLE Karyawan(
    nik VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(45) NOT NULL,
    id_dept VARCHAR(10) NOT NULL,
    sup_nik VARCHAR(10) DEFAULT NULL,
    gaji_pokok INT
    );

    INSERT INTO Karyawan (nik, nama, id_dept, sup_nik, gaji_pokok) VALUES
    ('N01', 'Ari', 'D01', NULL, 2000000),
    ('N02', 'Dina', 'D01', NULL, 2500000),
    ('N03', 'Rika', 'D03', NULL, 2400000),
    ('N04', 'Ratih', 'D01', 'N01', 3000000),
    ('N05', 'Riko', 'D01', 'N01', 2800000),
    ('N06', 'Dani', 'D02', NULL, 2100000),
    ('N07', 'Anis', 'D02', 'N06', 5000000),
    ('N08', 'Dika', 'D02', 'N06', 4000000),
    ('N09', 'Raka', 'D03', 'N06', 2000000);
    SELECT * FROM Karyawan;
    ```

    Output Tabel Karyawan :

    ![img.5](gambar/3.png)


* Script SQL berdasarkan Tabel Project

    ```sql
    CREATE TABLE Project(
    id_proj VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(45) NOT NULL,
    tgl_mulai DATETIME,
    tgl_selesai DATETIME,
    status TINYINT(1)
    );

    INSERT INTO Project (id_proj, nama, tgl_mulai, tgl_selesai, status) VALUES
    ('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
    ('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
    ('PJ03', 'C', '2019-03-21', '2019-05-10', '1');
    SELECT * FROM Project;
    ```

    Output Tabel Project :

    ![img.6](gambar/4.png)


* Script SQL berdasarkan Tabel Project Detail

    ```sql
    CREATE TABLE Project_detail(
    id_proj VARCHAR(10) NOT NULL,
    nik VARCHAR(10) NOT NULL
    );

    INSERT INTO Project_detail (id_proj, nik) VALUES
    ('PJ01', 'N01'),
    ('PJ01', 'N02'),
    ('PJ01', 'N03'),
    ('PJ01', 'N04'),
    ('PJ01', 'N05'),
    ('PJ01', 'N07'),
    ('PJ01', 'N08'),
    ('PJ02', 'N01'),
    ('PJ02', 'N03'),
    ('PJ02', 'N05'),
    ('PJ03', 'N03'),
    ('PJ03', 'N07'),
    ('PJ03', 'N08');
    SELECT * FROM Project_detail;
    ```
    
    Output Tabel Project Detail :

    ![img.7](gambar/5.png)


# LATIHAN PRAKTIKUM 7

1. Tampilkan data karyawan yang bekerja pada departemen yang sama dengan karyawan yang bernama Dika

    Script :

    ```sql
    SELECT nik, nama, id_dept FROM Karyawan WHERE id_dept = (SELECT id_dept FROM Karyawan WHERE nama = 'Dika');
    ```

    Output :

    ![img.8](gambar/6.png)

2. Tampilkan data karyawan yang gajinya lebih besar dari rata-rata gaji semua karyawan. Urutkan menurun berdasarkan besaran gaji

    Script :

    ```sql
    SELECT nik, nama, id_dept, gaji_pokok FROM karyawan WHERE gaji_pokok > (SELECT AVG(gaji_pokok) FROM Karyawan) ORDER BY gaji_pokok DESC;
    ```

    Output :

    ![img.9](gambar/7.png)

3. Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departmen yang sama dengan karyawan dengan nama yang mengandung huruf 'K'.

    Script :

    ```sql
    SELECT nik, nama FROM Karyawan WHERE id_dept IN (SELECT id_dept FROM Karyawan WHERE nama LIKE '%K%');
    ```

    Output :

    ![img.10](gambar/8.png)

4. Tampilkan data karyawan yang bekerja pada departemen yang ada di Kantor pusat.

    Script :

    ```sql
    SELECT karyawan.nik, karyawan.nama, karyawan.id_dept FROM karyawan JOIN departemen ON karyawan.id_dept = departemen.id_dept WHERE departemen.id_p = 'P01';
    ```

    Output :

    ![img.11](gambar/9.png)

5. Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di departmen yang sama dengan karyawan dengan nama yang mengandung huruf 'K' dan yang gajinya lebih besar dari rata-rata gaji semua karyawan

    Script :

    ```sql
    SELECT DISTINCT k1.nik, k1.nama FROM karyawan k1 JOIN karyawan k2 ON k1.id_dept = k2.id_dept WHERE k1.gaji_pokok > (SELECT AVG(gaji_pokok) FROM karyawan WHERE nama LIKE '%K%');
    ```

    Output :

    ![img.12](gambar/10.png)