# Sistem Komisi
## 🛠 Teknologi
- Backend: Laravel 12 (REST API)
- Frontend: React.js
- UI Framework: Bootstrap 5
- HTTP Client: Axios
- API Client: Postman

## 📁 Struktur Folder
- `/backend` → Laravel API
- `/frontend` → React frontend (menggunakan Bootstrap + Axios)
- `api-komisi.postman_collection.json` → Postman Collection

---

##  Cara Menjalankan

### Backend (Laravel 12)
cd backend
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
php artisan serve

### Frontend (React.js)
cd frontend
npm install
npm run dev


### Modifikasi FrontEnd Tambahan
-  Menambah Fitur Search Di Komisi Dan Penjualan
- Menambah Status Dan Dinamis Button Di Penjualan
- Menambah download Struk Di Pembayaran Jika Lunas