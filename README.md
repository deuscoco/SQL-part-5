# 📘 Basis Data Part 5 – GROUP BY & CASE WHEN


---

## 📌 Pendahuluan

Pada **Basis Data Part 5**, materi berfokus pada penggunaan klausa **GROUP BY** untuk melakukan pengelompokan data serta penggunaan **CASE WHEN** untuk membuat logika kondisi di dalam query SQL. Materi ini sangat penting dalam pembuatan laporan dan analisis data, khususnya untuk menghitung total, rata-rata, dan klasifikasi data.

Dokumentasi ini disusun dalam format **Markdown** agar dapat langsung digunakan sebagai **README di GitHub**, serta telah dilengkapi dengan **jawaban seluruh quiz** sesuai modul.

---

## 1️⃣ Pengenalan GROUP BY

`GROUP BY` digunakan untuk mengelompokkan baris data yang memiliki nilai sama pada satu atau lebih kolom.

### Contoh GROUP BY

```sql
SELECT status
FROM orders
GROUP BY status;
```

Query di atas akan menampilkan daftar status tanpa duplikasi.

---

## 2️⃣ GROUP BY dengan Aggregate Function

`GROUP BY` sering digunakan bersama fungsi aggregate seperti `SUM()`, `COUNT()`, dan `AVG()`.

### Contoh

```sql
SELECT status, COUNT(*) AS total_order
FROM orders
GROUP BY status;
```

```sql
SELECT orderNumber,
       SUM(quantityOrdered * priceEach) AS total
FROM orderdetails
GROUP BY orderNumber;
```

---

## 3️⃣ CASE WHEN

`CASE WHEN` digunakan untuk membuat kondisi logika di dalam query SQL.

### Contoh Sintaks

```sql
SELECT ColumnName1,
       ColumnName2,
       CASE
         WHEN condition1 THEN result1
         WHEN condition2 THEN result2
         ELSE result
       END AS alias
FROM TableName;
```

---

## 📝 Quiz 1

### Soal

Dengan menggunakan data pada tabel `orderdetails`, buat query yang:

* Menggunakan fungsi aggregate `SUM(quantityOrdered * priceEach)`
* Menambahkan kolom `remark` menggunakan `CASE WHEN`

Ketentuan remark:

* `>= 50000` → **Target Achieved**
* `<= 20000` → **Less Performed**
* Selain itu → **Follow Up**

---

### ✅ Jawaban Quiz 1

```sql
SELECT
    orderNumber,
    SUM(quantityOrdered * priceEach) AS total,
    CASE
        WHEN SUM(quantityOrdered * priceEach) >= 50000 THEN 'Target Achieved'
        WHEN SUM(quantityOrdered * priceEach) <= 20000 THEN 'Less Performed'
        ELSE 'Follow Up'
    END AS remark
FROM orderdetails
GROUP BY orderNumber;
```

---

## 📝 Quiz 2

### Soal

Buat laporan dari tabel `ms_transaksi` dengan ketentuan:

1. Total seluruh penjualan (revenue)
2. Total quantity seluruh produk yang terjual
3. Total quantity dan total revenue untuk setiap kode produk
4. Rata-rata total belanja per kode pelanggan
5. Tambahkan kolom `kategori`:

   * **High**: > 300.000
   * **Medium**: 100.000 – 300.000
   * **Low**: < 100.000

---

### ✅ Jawaban Quiz 2

#### 1️⃣ Total Revenue & Total Quantity

```sql
SELECT
    SUM(total) AS total_revenue,
    SUM(qty) AS total_quantity
FROM ms_transaksi;
```

---

#### 2️⃣ Total Quantity & Revenue per Kode Produk

```sql
SELECT
    kode_produk,
    SUM(qty) AS total_qty,
    SUM(total) AS total_revenue
FROM ms_transaksi
GROUP BY kode_produk;
```

---

#### 3️⃣ Rata-Rata Total Belanja per Kode Pelanggan

```sql
SELECT
    kode_pelanggan,
    AVG(total) AS rata_rata_belanja
FROM ms_transaksi
GROUP BY kode_pelanggan;
```

---

#### 4️⃣ Kategori Revenue

```sql
SELECT
    kode_pelanggan,
    SUM(total) AS total_revenue,
    CASE
        WHEN SUM(total) > 300000 THEN 'High'
        WHEN SUM(total) BETWEEN 100000 AND 300000 THEN 'Medium'
        ELSE 'Low'
    END AS kategori
FROM ms_transaksi
GROUP BY kode_pelanggan;
```

---

## ✅ Penutup

Dengan memahami penggunaan `GROUP BY` dan `CASE WHEN`, kita dapat membuat laporan data yang terstruktur dan informatif langsung dari database. Materi ini menjadi dasar penting sebelum mempelajari analisis data lanjutan seperti `HAVING`, `JOIN`, dan subquery.

---

## 🔗 Referensi

* [https://docs.google.com/document/d/1XJjPKM6Yi42rRjmvWBvewbik7Hjm4j-xeYWhed_3VYc/edit?usp=sharing]
* [https://www.mysql.com](https://www.mysql.com)
* [https://www.postgresql.org](https://www.postgresql.org)
* [https://learn.microsoft.com/sql](https://learn.microsoft.com/sql)
