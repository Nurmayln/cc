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

## 🔧 Troubleshooting

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
## 📌 Praktikum 04 - Menghubungkan React ke Flask

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Menyiapkan Backend dengan Flask

Pastikan Anda telah menginstal Python dan membuat virtual environment sebelum menjalankan perintah berikut:

```sh
cd backend
python -m venv venv
.env\Scripts\activate  # Untuk Windows
pip install flask flask-cors
```

Buat file `backend/app.py` dan tambahkan kode berikut:

```python
from flask import Flask, jsonify
from flask_cors import CORS  # Mengatasi masalah CORS

app = Flask(__name__)
CORS(app)

@app.route('/')
def home():
    return jsonify({"message": "Hello from Flask!"})

@app.route('/api/data')
def get_data():
    return jsonify({"data": "Hello from Flask API"})

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

Jalankan backend dengan perintah:

```sh
python backend/app.py
```

Buka browser dan akses:

```
http://localhost:5000/api/data
```

Jika berhasil, Anda akan melihat JSON:

```json
{"data": "Hello from Flask API"}
```

---

### 2️⃣ Menyiapkan Frontend dengan React

Pindah ke direktori frontend dan buat proyek React:

```sh
cd frontend
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
```

Buka `src/App.jsx` dan ubah menjadi:

```jsx
import React, { useState, useEffect } from 'react';

function App() {
    const [apiData, setApiData] = useState(null);

    useEffect(() => {
        fetch('http://localhost:5000/api/data')
            .then(response => response.json())
            .then(data => setApiData(data.data))
            .catch(error => console.error('Error fetching data:', error));
    }, []);

    return (
        <div style={{ textAlign: 'center', marginTop: '50px' }}>
            <h1>React & Flask Integration</h1>
            <p>{apiData ? apiData : "Loading data..."}</p>
        </div>
    );
}

export default App;
```

---

### 3️⃣ Menjalankan Aplikasi React

```sh
npm run dev
```

Pastikan terminal menampilkan informasi seperti:

```
Local: http://127.0.0.1:5173/
```

Buka URL tersebut di browser untuk melihat hasilnya.

---

## 🖼️ Hasil Tampilan

Tampilan yang seharusnya muncul di browser:



---

## 🔧 Troubleshooting Tips

🔴 **Flask tidak merespons di React (CORS error)**

Pastikan Flask-CORS sudah diinstal dan `CORS(app)` sudah ditambahkan di `app.py`.

```sh
pip install flask-cors
```

🔴 **React tidak menampilkan data**

- Periksa apakah backend berjalan dengan benar dengan membuka `http://localhost:5000/api/data` di browser.
- Pastikan Anda menggunakan `npm run dev` di React, bukan `npm start`.

## 📌 Praktikum 05 - Integrasi Flask dengan PostgreSQL

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Instalasi Psycopg2 (Untuk Koneksi ke PostgreSQL)

Jalankan perintah berikut untuk menginstal **psycopg2-binary**:

```sh
pip install psycopg2-binary
```

---

### 2️⃣ Menyiapkan Database di pgAdmin Desktop

1. Buka **pgAdmin**.
2. Buat database baru dengan nama **test_db**.
3. Buat user baru sesuai kebutuhan.
4. Jalankan perintah SQL berikut untuk membuat tabel:

```sql
CREATE TABLE IF NOT EXISTS items (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  description TEXT
);
```

---

### 3️⃣ Menambahkan Fungsi CRUD di Flask

Tambahkan kode berikut ke dalam aplikasi Flask Anda untuk mengimplementasikan fungsi **GET** dan **POST**:

```python
from flask import Flask, request, jsonify
import psycopg2

app = Flask(__name__)

def get_db_connection():
    conn = psycopg2.connect(
        dbname='test_db',
        user='your_user',
        password='your_password',
        host='localhost'
    )
    return conn

@app.route('/api/items', methods=['GET'])
def get_items():
    conn = get_db_connection()
    cur = conn.cursor()
    cur.execute("SELECT id, name, description FROM items;")
    rows = cur.fetchall()
    cur.close()
    conn.close()
    
    items = [{"id": row[0], "name": row[1], "description": row[2]} for row in rows]
    return jsonify(items)

@app.route('/api/items', methods=['POST'])
def create_item():
    data = request.json
    name = data['name']
    description = data['description']
    
    conn = get_db_connection()
    cur = conn.cursor()
    cur.execute("INSERT INTO items (name, description) VALUES (%s, %s) RETURNING id;", (name, description))
    new_id = cur.fetchone()[0]
    conn.commit()
    cur.close()
    conn.close()
    
    return jsonify({"id": new_id, "name": name, "description": description}), 201

if __name__ == '__main__':
    app.run(debug=True)
```

---

### 4️⃣ Menjalankan Flask

Jalankan aplikasi Flask dengan perintah:

```sh
python app.py
```

Aplikasi akan berjalan di **http://127.0.0.1:5000/**.

---

### 5️⃣ Menguji Endpoint dengan Postman

Gunakan **Postman** untuk mengetes endpoint:

- **GET**: `http://127.0.0.1:5000/api/items`
- **POST**: `http://127.0.0.1:5000/api/items`
  - Body (JSON):
  ```json
  {
    "name": "Example Item",
    "description": "This is an example description."
  }
  ```

Jika berhasil, Anda akan mendapatkan respons JSON sesuai dengan data yang dimasukkan.

---

# 📌 Praktikum 06 - Dockerization Bagian 1 (Membuat Dockerfile untuk Flask)

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Persiapan Awal

Pastikan **Docker Desktop** telah berjalan sebelum menjalankan perintah Docker. Cek dengan perintah berikut:

```sh
docker info
```

Jika Docker belum berjalan, kemungkinan akan muncul error seperti ini:

```sh
ERROR: error during connect: Get "http://%2F%2F.%2Fpipe%2FdockerDesktopLinuxEngine/v1.47/info": open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified.
```

✅ **Cara Menjalankan Docker Desktop:**

1. **Buka aplikasi Docker Desktop** 🐳
2. **Tunggu hingga status "Docker is running" muncul** ✅

---

### 2️⃣ Membuat Dockerfile

Buat file `Dockerfile` di dalam folder `backend` dengan isi sebagai berikut:

```dockerfile
# backend/Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

---

### 3️⃣ Menyiapkan requirements.txt

Tambahkan isi berikut ke file `requirements.txt`:

```
flask
flask-cors
psycopg2-binary
```

---

### 4️⃣ Membangun Docker Image 🏗️

Jalankan perintah berikut di dalam folder `backend`:

```sh
cd backend
docker build -t flask-backend:1.0 .
```

---

### 5️⃣ Menjalankan Docker Container 🚀

Setelah image berhasil dibuat, jalankan container dengan perintah:

```sh
docker run -d -p 5000:5000 --name flask-container flask-backend:1.0
```

---

### 6️⃣ Verifikasi di Browser 🌐

Cek apakah API Flask berjalan dengan mengakses:

🔗 [http://localhost:5000](http://localhost:5000)

---

##








