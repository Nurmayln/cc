# Cloud Computing

## 📌 Praktikum 02 - Membuat API Sederhana dengan Flask

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Masuk ke Direktori Backend

```sh
cd backend
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

## 🛠️ Troubleshooting

🔴 **Error 'Module not found'** ➜ Pastikan virtual environment sudah diaktifkan.
🔴 **Port 5000 sudah digunakan** ➜ Jalankan Flask dengan port lain:

```sh
python app.py --port=5001
```

atau hentikan proses yang menggunakan port 5000.

---

## 📌 Praktikum 03 - Membuat Aplikasi Frontend Sederhana dengan React + Vite

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Membuat Proyek React dengan Vite

```sh
cd frontend
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

Setelah menjalankan `npm run dev`, salin URL lokal (misalnya, `http://127.0.0.1:5173/`) dari terminal dan buka di browser.

---

### 2️⃣ Membuat Halaman Sederhana

Buka `src/App.jsx` dan ganti konten default dengan:

```jsx
import React from 'react';

function App() {
  return (
    <div style={{ textAlign: 'center', marginTop: '50px' }}>
      <h1>Hello from React + Vite!</h1>
      <p>This is a simple React app built with Vite.</p>
    </div>
  );
}

export default App;
```

---

### 3️⃣ Menjalankan Aplikasi React + Vite

```sh
npm run dev
```

Pastikan terminal menampilkan informasi seperti:

```
Local: http://127.0.0.1:5173/
```

Akses aplikasi di browser menggunakan URL tersebut.

---

## 🖼️ Hasil Tampilan

Tampilan yang seharusnya muncul di browser:

![Tampilan Aplikasi](public/tampilan.png)

---

## 🔧 Troubleshooting Tips

🔴 **Error ENOSPC (terkait watcher limit)**

```sh
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

🔴 **Blank screen** ➜ Periksa kesalahan sintaks di file React (misalnya, lupa menutup tanda kurung `}`).

---






