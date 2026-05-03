# Write-up: SecureBank
<img width="610" height="152" alt="image" src="https://github.com/user-attachments/assets/78ce09b5-75fc-4833-9cca-4b76f5c7cf03" />

## 📝 Challenge Description
> Password admin sengaja dibuat sangat kuat
> biar player mau gak mau harus pakai teknik injection

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Medium

---

## 🔍 Discovery
Saat pertama kali masuk ke aplikasi akan menampilkan halaman login 
<img width="476" height="571" alt="image" src="https://github.com/user-attachments/assets/96753a07-f427-4656-8234-390e27e9e7eb" />

---

## 🚀 Exploitation Steps

### 1. Exploit with Injection
Karena sudah mendapatkan clue dari awal, bahwa injection kita coba dengan command sederhana sebagai berikut 
```
'OR'1'='1'--
```
<img width="476" height="571" alt="image" src="https://github.com/user-attachments/assets/23b3501b-34b7-4f02-878e-d99df9a83785" />
Penjelasan kenapa program tersebut bisa tembus karena tidak memiliki validasi yang memadai, sehingga ketika menerima input TRUE langsung dieksekusi command **OR'1'='1'--** adalah mengubah value user dengan **TRUE** dan melakukan command untuk passwordnya 

### 2. Finding the Flag
Setelah berhasil login dan halaman dimuat ulang halaman berisi flag akan muncul.
<img width="588" height="553" alt="image" src="https://github.com/user-attachments/assets/aaaa02a0-6670-45ef-8031-03ee607a8479" />

---

## 🚩 Flag
`REDLIMIT{sql_1nj3ct10n_byp4ss_l0g1n_w1th_0r_1=1}`

---
