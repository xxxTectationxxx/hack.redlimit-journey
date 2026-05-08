# Write-up: Fake_Phishing528
<img width="611" height="154" alt="image" src="https://github.com/user-attachments/assets/a7bc7ab7-0ab1-426d-b8e8-ab3a71dc9cb9" />


## 📝 Challenge Description
> Seorang investigator ditugaskan untuk menganalisis aktivitas sebuah threat actor yang diduga merupakan scammer
> yang memperjualbelikan data breach menggunakan Ethereum (ETH). Data yang ditemukan sangat terbatas, namun alamat
> wallet threat actor tersebut telah ditandai sebagai phishing di blockchain explorer dengan label "Fake_Phishing528".
> Tugasmu adalah mencari 3 transaksi terbesar dari threat actor dengan label "Fake_Phishing528" tersebut.
> Berikan transaction hash nya dalam format flag berikut:
> REDLIMIT{hash1_hash2_hash3}

---

## 📊 Details
- **Category:** Osint 
- **Difficulty:** Medium

---

## 🔍 Discovery
Ketika pertama kali melihat challenge kita langsung diberikan clue format flag dan bagaimana cara mendapatkannya yakni dengan mencari di blockchain traknsaksi terbesar ETH dengan nama **Fake_Phishing528** dengan format flag yaitu 
```

REDLIMIT{hash1_hash2_hash3}

```

---

## 🚀 Exploitation Steps

### 1. Searching with Google Dorking 
Searching dengan format berikut : 
``` "Fake_Phishing528" ```
<img width="1160" height="733" alt="image" src="https://github.com/user-attachments/assets/042008c4-ec81-4e60-9d62-e17ce5c622b8" />
Akan muncul etherscan.io yang menampilkna semua transaksi yang dilakukan oleh "Fake_Phishing528"


### 2. Filter the amount
Setelah membuka website langsung filter minimal 10 ETH amount untuk melihat jumlah terbesar transaksi :
<img width="1372" height="490" alt="image" src="https://github.com/user-attachments/assets/79ab9f9e-2604-476f-8fc7-dd021c69c749" />

### 3. Finding the Flag
Setelah didapati 3 transaksi terbesar yaitu : 
```
1. 0xd2736d59273e64b3b750eb768723384ec99ae60bbb41addd41951937bad4e446
Amount : 29.09820644 ETH

2. 0x3f7a3f787eb08f90daa3f292aea5222b6ab7160f9dcbd1a837c4951b88d6828e
Amount : 15.38340772 ETH

3. 0x4ff7d3d884c52ccbd75b09a87b1f8c8d26e051be5bf2497d9bb29522c53ef585
Amount : 11.61122503 ETH
```

---

## 🚩 Flag
`REDLIMIT{0xd2736d59273e64b3b750eb768723384ec99ae60bbb41addd41951937bad4e446_0x3f7a3f787eb08f90daa3f292aea5222b6ab7160f9dcbd1a837c4951b88d6828e_0x4ff7d3d884c52ccbd75b09a87b1f8c8d26e051be5bf2497d9bb29522c53ef585}`

---
