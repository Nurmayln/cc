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

## 📌 Praktikum 05 - Integrasi Flask dengan PostgreSQL

---

## 🛠️ Langkah-Langkah Praktikum

### 1️⃣ Instalasi Psycopg2 (Untuk Koneksi ke PostgreSQL)

```sh
pip install psycopg2-binary
```

### 2️⃣ Menyiapkan Database di pgAdmin Desktop

Buat Database baru dengan contoh `test_db` lalu kemudian buat user baru.

### 3️⃣ Membuat Table Baru

Jalankan perintah berikut untuk membuat tabel baru:

```sql
CREATE TABLE IF NOT EXISTS items (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  description TEXT
);
```

### 4️⃣ Menambahkan Fungsi CRUD pada Flask

Tambahkan kode berikut ke dalam aplikasi Flask:

```python
from flask import Flask, request, jsonify
import psycopg2

app = Flask(__name__)

def get_db_connection():
    conn = psycopg2.connect(
        dbname='test_db', user='your_user', password='your_password', host='localhost'
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
```

### 5️⃣ Menjalankan Flask

```sh
python app.py
```

### 6️⃣ Menggunakan Postman untuk Menguji Endpoint

Gunakan Postman untuk mengakses endpoint:

- **GET**: `http://localhost:5000/api/items` ➜ Mengambil semua data.
- **POST**: `http://localhost:5000/api/items` ➜ Menambahkan data baru dengan JSON body:

```json
{
  "name": "Item 1",
  "description": "Deskripsi item 1"
}
```

---

##

---

