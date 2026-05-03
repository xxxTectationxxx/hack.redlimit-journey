# Write-up: TokoSultan

## 📝 Challenge Description
> Kamu hanya punya saldo Rp 1.000 sedangkan barang yang dijual harganya Rp 1.000.000.000.
> Bagaimana cara mendapatkan flag?

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery
Saat pertama kali masuk ke aplikasi terlihat saldo dan barang yang bisa dibeli
<img width="886" height="402" alt="image" src="https://github.com/user-attachments/assets/9958de94-2d4d-4208-8434-b7e7a998f4db" />


Ketika dengan Polos untuk melakukan pembelian akan terjadi kegagalan karena saldo tidak mencukupi
<img width="864" height="486" alt="image" src="https://github.com/user-attachments/assets/a10c24b0-598d-4317-976c-b5b1d81cac05" />


---

## 🚀 Exploitation Steps

### 1. Use Intercept
Langkah pertama adalah mempersiapkan proxy untuk menangkap request yang masuk,sebagai contoh disini menggunakan burpsuite dengan fitur **Intercept** untuk menangkap Request
<img width="829" height="453" alt="image" src="https://github.com/user-attachments/assets/7e21893c-2ce8-40b2-bdd5-e8679a383f6b" />

### 2. Modification Parameter
Setelah menangkap request disini kita bisa memodifikasi value harga agar sesuai dengan saldo kita
<img width="829" height="453" alt="image" src="https://github.com/user-attachments/assets/90b7b79b-d8fa-4355-9531-b8f53cea3186" />

### 3. Finding the Flag
Kemudian pilih forward dan kamu akan mendapatkan flag
<img width="848" height="541" alt="image" src="https://github.com/user-attachments/assets/16ed7369-a711-426d-9549-fbfe5ccf1d73" />


---

## 🚩 Flag
`REDLIMIT{p4r4m3t3r_t4mp3r1ng_1s_d4ng3r0us_4nd_fun_2026}`

---
