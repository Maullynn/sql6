# Soal Latihan Praktikum

## 1. Departemen Apa Saja Yang Terlibat Dalam Tiap-tiap Project.
Query ini digunakan untuk mengetahui departemen apa saja yang terlibat dalam setiap project.



```
SELECT Project.nama AS Project, GROUP_CONCAT(Departemen.nama) AS Departemen
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj;
```
## 2. Jumlah Karyawan Tiap Departemen Yang Bekerja Pada Tiap-tiap Project.
Query ini digunakan untuk mengetahui jumlah karyawan dari setiap departemen yang bekerja pada tiap project.



```
SELECT Project.nama AS Project, Departemen.nama AS Departemen, COUNT(*) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj, Departemen.id_dept;
```

## 3. Ada Berapa Project Yang Sedang Dikerjakan Oleh Departemen ***RnD***? (ket: project berjalan adalah yang statusnya 1).
Query ini digunakan untuk mengetahui berapa banyak project yang sedang dikerjakan oleh departemen RnD. Project yang sedang berjalan ditandai dengan status 1.

```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD' AND Project.status = 1;
```

## 4. Berapa banyak Project yang sedang dikerjakan oleh Ari ?
Query ini digunakan untuk mengetahui berapa banyak project yang sedang dikerjakan oleh karyawan bernama Ari. Project yang sedang berjalan ditandai dengan status 1.



```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```

## 5. Siapa Saja Yang Mengerjakan Project B ?
Query ini digunakan untuk mengetahui siapa saja karyawan yang mengerjakan project B.



```
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```
