# cc
# 📌 Praktikum 02 - Membuat API Sederhana dengan Flask

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Masuk ke Direktori Backend

```sh
cd cloud-project/backend
```

### 2️⃣ Membuat Virtual Environment

```sh
python -m venv venv
```

### 3️⃣ Mengaktifkan Virtual Environment

**Untuk Windows:**

```sh
venv\Scripts\activate
```

Jika menggunakan PowerShell dan ada error terkait izin eksekusi, jalankan:

```sh
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

**Untuk Linux/MacOS:**

```sh
source venv/bin/activate
```

### 4️⃣ Menginstal Flask

```sh
pip install Flask
```

Jika terjadi timeout saat instalasi, gunakan:

```sh
pip install Flask --default-timeout=100
```

Atau coba menggunakan mirror server yang lebih cepat:

```sh
pip install Flask -i https://pypi.doubanio.com/simple
```

### 5️⃣ Membuat Struktur Dasar Flask

Buat file `app.py` di dalam folder `backend`, lalu isi dengan kode berikut:

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def home():
    return jsonify({"message": "Hello from Flask!"})

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

### 6️⃣ Menjalankan Aplikasi Flask

```sh
python app.py
```

Buka browser dan akses:

- [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
- [http://localhost:5000/](http://localhost:5000/)

---

## 📂 Struktur Direktori yang Direkomendasikan (Opsional)

```
backend/
├─ venv/
├─ app.py
├─ requirements.txt
└─ ...
```

### 7️⃣ Membuat `requirements.txt` (Opsional)

Simpan daftar library yang dibutuhkan untuk mempermudah instalasi di lingkungan lain:

```sh
pip freeze > requirements.txt
```

Contoh isi `requirements.txt`:

```
Flask==3.1.0
Jinja2==3.1.5
Werkzeug==3.1.3
click==8.1.8
itsdangerous==2.2.0
```

Untuk menginstal semua dependensi yang tercantum di `requirements.txt`:

```sh
pip install -r requirements.txt
```

---

## 🛠️ Troubleshooting

🔴 **Error 'Module not found'** ➜ Pastikan virtual environment sudah diaktifkan.\
🔴 **Port 5000 sudah digunakan** ➜ Jalankan Flask dengan port lain:

```sh
python app.py --port=5001
```

atau hentikan proses yang menggunakan port 5000.

---



