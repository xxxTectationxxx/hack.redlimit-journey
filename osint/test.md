# Write-up: test
<img width="615" height="145" alt="Screenshot from 2026-05-08 10-08-30" src="https://github.com/user-attachments/assets/fa8f1245-8cab-4e91-969d-f07bdda30623" />


## 📝 Challenge Description
> === [ INTERCEPTED PROFILE DUMP: RedLimit ] ===
>
> Username: @RedLimit
> Status: "Mencari kebenaran di tumpukan jerami digital."
> Bio:
> "Suka kriptografi dan fotografi.
> Jangan coba-coba meretas saya.
> Part 1: UkVETElNSVR7"
>
> Recent Activity Log:
> [2023-10-27 14:00] Uploaded file: 'secret_view.jpg' (deleted)
> [2023-10-27 14:05] Updated status: "Koordinatku ada di mana-mana."
> [2023-10-27 14:10] Posted comment:
> "Guys, aku lupa password emailku. Hint-nya adalah nama kucingku ditambah underscore.
> Kucingku namanya 'OS1NT'.
> Btw, Part 2 kuncinya ada di sini tapi terbalik: _TNSI"
> 
> [2023-10-27 14:15] Emergency Note saved:
> "Ingat, bagian terakhir selalu yang paling sulit.
> Gunakan Hex untuk bicara denganku.
> Part 3: 5930557D"

---

## 📊 Details
- **Category:** Osint 
- **Difficulty:** Easy

---

## 🔍 Discovery
Ini adalah teka teki yang menarik, dimana ketika awal melihat langsung diberikan log dan hits untuk mendapatkan flagnya

---

## 🚀 Exploitation Steps

### 1. Decode Part1
Yang pertama bisa dilakukan adalah melakukan decode pada hits ini **Part 1: UkVETElNSVR7"** menggunakan CyberChef : 
<img width="815" height="549" alt="image" src="https://github.com/user-attachments/assets/2e586491-ca89-4c5d-8f8d-3a27bf695d7f" />
Sehingga didapati awalan flag yaitu : **REDLIMIT{**

### 2. Decode Part2
Yang kedua didapati Hint-nya adalah nama kucingku ditambah underscore.
> Kucingku namanya 'OS1NT'.
> Btw, Part 2 kuncinya ada di sini tapi terbalik: _TNSI">
> 
Sehingga dapat disimpulkan Menambahkan nama kucing dengan underscore dan pembalikan Kucing yang ada disini jadi didapati bahwa tengah flagnya berisi **OS1NT_ISNT_**

### 3. Decode Part 3
Ini clue untuk mendapatkan akhiran flagnya : 
> Gunakan Hex untuk bicara denganku.
> Part 3: 5930557D"
Kita bisa melakukan decode menggunakan hex menggunakan CyberChef dan didapati **Y0U}**
> <img width="815" height="549" alt="image" src="https://github.com/user-attachments/assets/73ce8215-3edf-402c-8afd-d9aa32ad5bde" />


---

## 🚩 Flag
`REDLIMIT{OS1NT_ISNT_Y0U}`

---
