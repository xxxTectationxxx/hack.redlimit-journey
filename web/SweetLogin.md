# Write-up: SweetLogin

## 📝 Challenge Description
> Kamu diberikan akses ke sebuah portal login.
> Tidak diperlukan brute force — cukup rasa ingin tahu.

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery 
Saat pertama kali masuk ke aplikasi Kamu akan melihat halaman login seperti berikut : 
<img width="715" height="550" alt="image" src="https://github.com/user-attachments/assets/59d7e1c6-da9a-499d-8ca1-3e92a409d1c5" />

Yang ketika username dan password yang dimasukkan salah akan menampilkan "Invalid Credentials"
<img width="673" height="485" alt="image" src="https://github.com/user-attachments/assets/6fb5f157-53a7-4f03-ab0d-1df28eb4d225" />

---

## 🚀 exploitation Steps

### 1. View Source
Langkah pertama adalah membuka **View Source** (Ctrl + U) dan code fullnya sebagai berikut:
<img width="790" height="432" alt="image" src="https://github.com/user-attachments/assets/f7619f79-bdca-47d0-a25e-596dade6d00e" />


### 2. Finding Credetials Public
Dari **View Source** sebelumnya didapati auth.js  
<img width="790" height="432" alt="image" src="https://github.com/user-attachments/assets/ce892b06-aa0c-43e1-9dda-946daf52e670" />

Yang berisi decode user dan pass : 
<img width="792" height="227" alt="image" src="https://github.com/user-attachments/assets/c5c5d230-02db-461a-af7e-e903452982a4" />

Setelah diperiksa menggunakan website "_https://www.dcode.fr/cipher-identifier_" diketahui bahwa code tersebut adalah base64
<img width="789" height="252" alt="image" src="https://github.com/user-attachments/assets/9c4645c7-7502-4567-8fea-eef4f47b454a" />

Lakukan Decode User : 
<img width="666" height="493" alt="image" src="https://github.com/user-attachments/assets/8e2947cc-071d-4734-9c45-9eaee6fb3ac4" />

Lakukan Decode Password : 
<img width="666" height="493" alt="image" src="https://github.com/user-attachments/assets/adee0239-b429-4cf3-b4f7-b1845acdbf8b" />

Setelah di decode menggunakan didapati user dan pass yaitu : 
user = admin 
pass = admin123

### 3. Login and Get the Flag
Setelah mendapati username dan password kamu bisa langsung login untuk mendapati flagnya
<img width="902" height="230" alt="image" src="https://github.com/user-attachments/assets/07d06f34-7ac1-4942-81c2-31beb8e21c00" />

---

## 🚩 Flag
`REDLIMIT{CLIENT_SIDE_SECURITY_IS_NOT_SECURITY}`

---
