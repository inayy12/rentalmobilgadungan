# rentalmobilgadungan

# ERD

# DDL 

### 1.MEMBUAT DATABASE
```
CREATE DATABASE rental_mobil;
```
### 2. MASUK KEDALAM DATABASE
```
USE rental_mobil;
```
### 3. MEMBUAT TABEL
```
CREATE TABLE customer (
    ->     id_customer VARCHAR (10) PRIMARY KEY,
    ->     nama_cs VARCHAR (45),
    ->     no_hp INT (15),
    ->     alamat VARCHAR (45),
    ->     email VARCHAR (45));
```
```
CREATE TABLE sopir (
    ->     id_sopir VARCHAR (10) PRIMARY KEY,
    ->     id_kendaraan VARCHAR (10),
    ->     nama_sp VARCHAR (45),
    ->     status_sp ENUM ('TERSEDIA', 'TIDAK TERSEDIA') NOT NULL);
```
```
CREATE TABLE kendaraan (
    ->      id_kendaraan VARCHAR (10) PRIMARY KEY,
    ->      merk VARCHAR (45),
    ->      warna VARCHAR (45),
    ->      status_kdr ENUM ('TERSEDIA', 'TIDAK TERSEDIA') NOT NULL,
    ->      harga_sewa INT);
```
```
CREATE TABLE transaksi (
    ->      id_transaksi VARCHAR (10) PRIMARY KEY,
    ->      id_customer VARCHAR (10),
    ->      id_sopir VARCHAR (10),
    ->      id_kendaraan VARCHAR (10),
    ->      tgl_pembayaran DATE,
    ->      tgl_sewa DATE,
    ->      tgl_kembali DATE,
    ->      status_transaksi VARCHAR (45),
    ->      total_harga INT,
    ->      metode_pembayaran VARCHAR (45));
```
### 4. MENAMBAHKAN INDEX KEY
```
ALTER TABLE transaksi ADD CONSTRAINT FOREIGN KEY (id_customer) REFERENCES customer (id_customer);
ALTER TABLE transaksi ADD CONSTRAINT FOREIGN KEY (id_sopir) REFERENCES sopir (id_sopir);
ALTER TABLE transaksi ADD CONSTRAINT FOREIGN KEY (id_kendaraan) REFERENCES kendaraan (id_kendaraan);
ALTER TABLE sopir ADD CONSTRAINT FOREIGN KEY (id_kendaraan) REFERENCES kendaraan (id_kendaraan);
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/bf3a2570-3e93-4f40-85c4-723ae2e40b1d)

# SQL CURD
### CREATE
```
INSERT INTO customer (id_customer, nama_cs, no_hp, alamat, email)
    ->      VALUES
    ->      ('CS001', 'ARUL', '089754637285', 'JL.ANGGREK', 'arul@gmail.com'),
    ->      ('CS002', 'INAY', '089654236789', 'JL.MAWAR', 'inay@gmail.com'),
    ->      ('CS003', 'RANI', '089172634563', 'JL.MELATI', 'rani@gmail.com'),
    ->      ('CS004', 'FIA', '089876543245', 'JL.KEMUNING', 'fia@gmail.com'),
    ->      ('CS005', 'FEBRI', '089764536276', 'JL.CURUG', 'febri@gmail.com');
```
```
INSERT INTO sopir (id_sopir, id_kendaraan, nama_sp, status_sp)
    ->      VALUES
    ->      ('SP001', 'KDR001', 'Janu', 'TERSEDIA'),
    ->      ('SP002', 'KDR002', 'Rudi', 'TERSEDIA'),
    ->      ('SP003', 'KDR003', 'Siti', 'TERSEDIA'),
    ->      ('SP004', 'KDR004', 'Ahmad', 'TIDAK TERSEDIA'),
    ->      ('SP005', 'KDR005', 'Lina', 'TIDAK TERSEDIA');
```
```
INSERT INTO kendaraan (id_kendaraan, merk, warna, status_kdr, harga_sewa)
    -> VALUES
    -> ('KDR001', 'TOYOTA', 'HITAM', 'TERSEDIA', '100000'),
    -> ('KDR002', 'HYUNDAI', 'SILVER', 'TIDAK TERSEDIA', '500000'),
    -> ('KDR003', 'HONDA', 'MERAH', 'TERSEDIA', '300000'),
    -> ('KDR004', 'SUZUKI', 'HITAM', 'TIDAK TERSEDIA', '600000'),
    -> ('KDR005', 'PORSCHE', 'UNGUN', 'TERSEDIA', '3000000');
```
```
INSERT INTO transaksi (id_transaksi, id_customer, id_sopir, id_kendaraan, tgl_pembayaran, tgl_sewa, tgl_kembali, status_transaksi, total_harga, metode_pembayaran)
    -> VALUES
    -> ('01', 'CS002', 'SP001', 'KDR004', '2023-01-02', '2023-01-02', '2023-01-03', 'SELESAI', '600000', 'CASH'),
    -> ('02', 'CS004', 'SP003', 'KDR005', '2023-02-05', '2023-02-05', '2023-02-06', 'SELESAI', '3000000', 'KREDIT'),
    -> ('03', 'CS005', 'SP004', 'KDR003', '2023-03-20', '2023-03-21', '2023-03-22', 'SELESAI', '600000', 'CASH'),
    -> ('04', 'CS003', 'SP001', 'KDR005', '2023-11-15', '2023-12-15', '2023-12-16', 'SELESAI', '6000000', 'CASH'),
    -> ('05', 'CS001', 'SP002', 'KDR001', '2023-05-05', '2023-05-06', '2023-05-07', 'SELESAI', '200000', 'DEBIT'),
    -> ('06', 'CS002', 'SP001', 'KDR005', '2023-06-17', '2023-06-17', '2023-06-18', 'SELESAI', '6000000', 'CASH');
```

### READ

```
SELECT * FROM customer;
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/5b112f5b-ccf4-4885-bdee-559266b2ad39)

```
SELECT * FROM sopir;
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/03270eb4-ede1-4487-bd75-0fed73f5cad8)

```
SELECT * FROM kendaraan;
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/6a38ee65-89b6-4a0d-a46b-0eca49ba14db)

```
SELECT * FROM transaksi;
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/b0c5b6d2-94a7-474d-9365-90822c4c1ed3)

### UPDATE

```
UPDATE customer SET email = 'sahrul@gmail.com' WHERE id_customer = 'CS001';
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/32a5614f-9360-4266-ad70-909780462769)

```
UPDATE sopir SET status_sp = 'TERSEDIA' WHERE id_sopir = 'SP004';
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/ed9fdae0-600e-4664-8b77-b8d220e80296)

```
UPDATE kendaraan SET warna = 'BIRU' WHERE id_kendaraan = 'KDR005';
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/9dd4bc05-27bd-47c4-a31d-c7e06ad756ff)

```
UPDATE transaksi SET metode_pembayaran = 'CASH' WHERE id_transaksi = '02';
```
![image](https://github.com/inayy12/rentalmobilgadungan/assets/115867315/867ef90d-9f74-4d0a-9a21-a6ade39790d3)

### DELETE


# SQL JOIN



