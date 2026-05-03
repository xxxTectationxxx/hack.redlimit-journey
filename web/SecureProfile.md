# Write-up: SecureProfile

## 📝 Challenge Description
> Selamat datang di SecureProfile!
> Login dengan akun guest yang sudah disediakan

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery
Saat pertama kali masuk ke aplikasi akan ada halaman login yang menyediakan username dan passwordnya
<img width="600" height="541" alt="image" src="https://github.com/user-attachments/assets/07b9deb3-5283-42ff-9a9e-6bc3778b1883" />


---

## 🚀 Exploitation Steps

### 1. Check Login
Login menggunakan username dan password tersebut, setelah login halamannya akan tampil seperti berikut 
<img width="698" height="722" alt="image" src="https://github.com/user-attachments/assets/c4017409-4ab6-4e37-a2fd-2e42cd200dd1" />


### 2. Modification ID User
Modifikasi ID user yang sebelumnya **2** menjadi **1** karena user diawali dari angka **1** dan biasanya admin
<img width="769" height="620" alt="image" src="https://github.com/user-attachments/assets/17867f18-00cd-4d75-96df-7d0f083dc737" />

### 3. Finding the Flag
Setelah melakukan modifikasi ternyata benar ID user **1** benar admin
<img width="832" height="776" alt="image" src="https://github.com/user-attachments/assets/e7d30bbe-79ae-4189-b908-13ecf66cbb1e" />


---

## 🚩 Flag
`REDLIMIT{1d0r_4cc3ss_4dm1n_pr0f1l3_e4sy_w1n}`

---
