# Write-up: Privilege1

## 📝 Challenge Description
> Sebuah sistem manajemen sederhana memiliki beberapa tingkatan pengguna.  
> Kamu berhasil masuk menggunakan akun yang tersedia, namun terasa ada sesuatu yang tidak diperlihatkan kepadamu.  
> Terkadang, batasan hanyalah ilusi — jika kamu tahu di mana harus melihat.

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery
Saat pertama kali masuk ke aplikasi akan menampilkan 2 menu yaitu Home dan Flag
<img width="959" height="183" alt="image" src="https://github.com/user-attachments/assets/2c40454c-b3b6-4028-9611-59d8dee66c41" />

Dan Ketika Membuka menu flag memberikan clue "Role selain admin dilarang akses!" 
Berdasarkan analisis awal, menunjukkan bahwa yang bisa melihat flag hanya admin dan user biasa tidak bisa membukanya

---

## 🚀 exploitation Steps

### 1. Inspecting the Environment
Langkah pertama adalah membuka **Developer Tools** (F12) dan memeriksa bagian **Application** > **Cookies**. Ditemukan sebuah cookie dengan parameter sebagai berikut:
<img width="782" height="93" alt="image" src="https://github.com/user-attachments/assets/40cf8fe2-d782-4a27-a57a-e2aca5e90bb1" />

Kemudian identifikasi value melakukan decode menggunakan code apa, dengan menggunakan web berikut "https://www.boxentriq.com/analysis/cipher-identifier" dan didapati bahwa valuenya merupakan base64
<img width="744" height="370" alt="image" src="https://github.com/user-attachments/assets/08062698-bf68-442c-a4c0-bfab29c144db" />

Lakukan decode untuk melihat value aslinya melalui tools decode base64
<img width="669" height="492" alt="image" src="https://github.com/user-attachments/assets/f50bce72-cdbd-43a1-8d12-836376dbc73d" />

Karena sebelumnya yang bisa masuk hanya admin disini ubah role yang sebelumnya "guest" menjadi "admin" kemudian encode lagi menjadi base64
<img width="669" height="572" alt="image" src="https://github.com/user-attachments/assets/240db986-e83e-4184-a6b8-b3a9c0fcaf1e" />



### 2. Privilege Escalation
Berdasarkan value yang didapatkan sebelumnya kamu bisa ubah value pada browser kamu 
<img width="783" height="58" alt="image" src="https://github.com/user-attachments/assets/26f10ccc-9ea8-4d12-bbcc-50e09d1404d4" />

### 3. Finding the Flag
Setelah halaman dimuat ulang dengan role baru, menu navigasi admin muncul atau sebuah pesan rahasia terbuka yang berisi flag.

---

## 🚩 Flag
`REDLIMIT{Privilege_Escalation_Vulnerability_Broken_Access_Control}`

---
